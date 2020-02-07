<template>
  <div class="table">
    <app-popup
      v-if="filterPopup"
      @popupToggle="popupToggle"
      @applyChange="applyChange"
      :filterParametrs="filterParametrs.urlTypeSearch"
    ></app-popup>
    <app-spinner v-if="loading"></app-spinner>
    <app-title
      :chekedCount="getCountOfSelecetdItems"
      @deleteSelectedSitemaps="deleteSelectedSitemaps"
    ></app-title>
    <app-filters
      @setFilterParametrs="setFilterParametrs"
      @popupToggle="popupToggle"
    ></app-filters>
    <app-header
      :numberOfRows="displayArray.length"
      @selectAllSitemaps="selectAllSitemaps"
      :allChecked="allChecked"
    ></app-header>
    <tbody>
      <app-body
        v-for="row in displayArray"
        :siteInfo="row"
        :key="row.id"
        @deleteItem="deleteSitemap"
        @selectSitemap="selectSitemap"
      ></app-body>
    </tbody>
  </div>
</template>

<script>
import Spinner from "./Spinner";
import Title from "./TableTitle";
import Filters from "./TableFilters";
import Header from "./TableHeader";
import Body from "./TableBody";
import PopupSelect from "./PopupSelect";
export default {
  components: {
    appSpinner: Spinner,
    appTitle: Title,
    appFilters: Filters,
    appHeader: Header,
    appBody: Body,
    appPopup: PopupSelect
  },
  data: function() {
    return {
      fetchedArray: [],
      displayArray: [],
      loading: true,
      allChecked: false,
      filterPopup: false,
      filterParametrs: {
        sitemapStatus: "all",
        urlPath: "",
        urlTypeSearch: "cont"
      }
    };
  },
  methods: {
    selectSitemap(index) {
      this.fetchedArray = this.fetchedArray.map(el => {
        if (el.id == index) {
          el.checked = !el.checked;
        }
        return el;
      });
      this.displayArray = this.fetchedArray.map(el => {
        if (this.displayArray[el.id]) {
          el.checked = this.fetchedArray[el.id].checked;
        }
        return el;
      });
      this.allChecked = false;
      //  console.log(this.displayArray)
    },
    selectAllSitemaps(status) {
      this.allChecked = !status;
      this.fetchedArray = this.fetchedArray.map(el => {
        el.checked = !status;
        return el;
      });

      this.displayArray = this.displayArray.map(el => {
        el.checked = !status;
        return el;
      });
    },
    deleteSitemap(index) {
      this.fetchedArray = this.fetchedArray.filter(el => el.id != index);
      this.displayArray = JSON.parse(JSON.stringify(this.fetchedArray));
    },
    deleteSelectedSitemaps() {
      this.fetchedArray = this.fetchedArray.filter(el => el.checked != true);
      this.displayArray = this.displayArray.filter(el => el.checked != true);
      this.allChecked = false;
    },
    setFilterParametrs(url, type) {
      this.filterParametrs.urlPath = url.trim().toLowerCase();
      this.filterParametrs.sitemapStatus = type;
      this.filterDate();
      this.popupOff();
    },
    popupToggle() {
      this.filterPopup = !this.filterPopup;
    },
    popupOff() {
      this.filterPopup = false;
    },
    applyChange(newVel) {
      this.filterParametrs.urlTypeSearch = newVel;
      this.popupToggle();
      this.filterDate();
    },
    filterDate() {
      let { sitemapStatus, urlPath, urlTypeSearch } = this.filterParametrs;

      if (sitemapStatus == "all") {
        this.displayArray = JSON.parse(JSON.stringify(this.fetchedArray));
      } else if (sitemapStatus == "suc") {
        this.displayArray = this.fetchedArray.filter(el => el.errors == 0);
      } else if (sitemapStatus == "err") {
        this.displayArray = this.fetchedArray.filter(el => el.errors != 0);
      }
      if (urlPath == "") {
        //this.displayArray = JSON.parse(JSON.stringify(this.fetchedArray));
      } else if (urlTypeSearch == "cont") {
        this.displayArray = this.displayArray.filter(el =>
          el.path.match(/\/([^/]+)\/?$/)[1].includes(urlPath)
        );
      } else if (urlTypeSearch == "notcont") {
        this.displayArray = this.displayArray.filter(
          el => !el.path.match(/\/([^/]+)\/?$/)[1].includes(urlPath)
        );
      } else if (urlTypeSearch == "exact") {
        this.displayArray = this.displayArray.filter(el =>
          el.path.match(/\/([^/]+)\/?$/)[1].startsWith(urlPath)
        );
      }
    }
  },
  mounted: function() {
    this.$http
      .get("https://semalt.tech/dev/api/v1/example/test/")
      .then(response => {
        return response.json();
      })
      .then(sitemaps => {
        this.fetchedArray = sitemaps.result.sitemap;
        this.fetchedArray.map((el, id) => {
          this.$set(el, "checked", false);
          this.$set(el, "id", id);
        });
        this.displayArray = JSON.parse(JSON.stringify(this.fetchedArray));
        this.loading = false;
      });
  },
  computed: {
    getCountOfSelecetdItems: function() {
      return this.fetchedArray.filter(el => el.checked == true).length;
    }
  }
};
</script>

<style>
.table {
  position: relative;
  font-family: Roboto;
  width: 920px;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 16px;
  text-align: center;
  background: #ffffff;
  color: #37474f;
  border: 1px solid #c2cfe0;
  box-sizing: border-box;
  border-collapse: collapse;
  border-radius: 5px;
}

.green {
  color: #2ac9a1;
}
.blue {
  color: #0288d1;
}
.red {
  color: #fb6868;
}
</style>
