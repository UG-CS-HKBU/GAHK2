<template>
  <div class="container">
    <h2>Here shows the details of the course</h2>
    <o-table
      :data="isEmpty ? [] : data"
      :bordered="isBordered"
      :striped="isStriped"
      :narrowed="isNarrowed"
      :hoverable="isHoverable"
      :loading="isLoading"
      :focusable="isFocusable"
      :mobile-cards="hasMobileCards"
    >
      <o-table-column field="id" label="ID" width="40" numeric v-slot="props">
        {{ props.row.id }}
      </o-table-column>
      <o-table-column field="code" label="課程編碼" v-slot="props">
        {{ props.row.code }}
      </o-table-column>
      <o-table-column field="category" label="體操類別" v-slot="props">
        {{ props.row.category }}
      </o-table-column>
      <o-table-column field="difficulty" label="項目難度" v-slot="props">
        {{ props.row.difficulty }}
      </o-table-column>
      <o-table-column field="coach" label="教練" v-slot="props">
        {{ props.row.coach }}
      </o-table-column>
      <o-table-column field="Sdate" label="開始日期" v-slot="props">
        {{ props.row.dates.Sdate }}
      </o-table-column>
      <o-table-column field="Edate" label="結束日期" v-slot="props">
        {{ props.row.dates.Edate }}
      </o-table-column>
      <!-- <o-table-column field="dates" label="上課日期" v-slot="props">
        {{ props.row.dates }}
      </o-table-column> -->
      <o-table-column field="week" label="星期" v-slot="props">
        {{ props.row.week }}
      </o-table-column>
      <!-- <o-table-column field="Uage" label="年齡上限" v-slot="props">
        {{ props.row.Uage }}
      </o-table-column>
      <o-table-column field="Lage" label="年齡下限" v-slot="props">
        {{ props.row.Lage }}
      </o-table-column> -->
      <o-table-column field="gym" label="體育館" v-slot="props">
        {{ props.row.gym }}
      </o-table-column>
      <o-table-column field="gym1" label="場地" v-slot="props">
        {{ props.row.gym1 }}
      </o-table-column>
      <o-table-column field="gym1" label="名額" v-slot="props">
        {{ props.row.quato }}
      </o-table-column>
      <o-table-column field="gym1" label="費用" v-slot="props">
        {{ props.row.fee }}
      </o-table-column>
      <o-table-column field="intro" label="内文" v-slot="props">
        {{ props.row.intro }}
      </o-table-column>
    </o-table>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
export default {
  data() {
    return {
      data: [],
      isEmpty: false,
      isBordered: false,
      isStriped: false,
      isNarrowed: false,
      isHoverable: false,
      isFocusable: false,
      isLoading: false,
      hasMobileCards: true,
    };
  },
  mounted() {
    fetch("http://localhost:1337/course/read/" + this.$route.params.id)
      .then((res) => res.json())
      .then((data) => (this.data = data))
      .catch((err) => console.log(err.message));
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
