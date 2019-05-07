<template>
  <mu-form ref="form" :model="form">
    <mu-form-item label="Latitude" prop="lat" :rules="lat_rules">
      <mu-text-field v-model="form.lat" prop="lat" placeholder="eg: 41.5231" type="number"></mu-text-field>
    </mu-form-item>

    <mu-form-item label="Longitude" prop="lon" :rules="lon_rules">
      <mu-text-field v-model="form.lon" prop="lon" placeholder="eg: 123.0125" type="number"></mu-text-field>
    </mu-form-item>

    <mu-form-item label="Maidenhead Grid">
      <mu-text-field v-model="mg" placeholder="Grid Coordinate" readonly></mu-text-field>
    </mu-form-item>
  </mu-form>
</template>

<script>
  const s1 = "ABCDEFGHIJKLMNOPQR";
  const s2 = "0123456789";
  const s3 = "abcdefghijklmnopqrstuvwx";
  const s4 = s2;
  const s5 = s3;
  const s6 = s4;

  function iter(ratio, charset) {
    let i = ratio * charset.length;
    let _i = Math.floor(i);
    return {
      char: charset.charAt(_i),
      rest: i - _i
    }
  }

  export default {
    name: "PageGridConv",
    data() {
      return {
        form: {
          lat: 41.5231,
          lon: 123.0125,
        },
        lon_rules: [
          {validate: (val) => !!val, message: "do not leave it empty"},
          {validate: (val) => parseFloat(val) + "" === val + "", message: "please input a valid decimal"},
          {validate: (val) => val >= -180 && val < 180, message: "your input shall be in [-180, 180)"},
        ],
        lat_rules: [
          {validate: (val) => !!val, message: "do not leave it empty"},
          {validate: (val) => parseFloat(val) + "" === val + "", message: "please input a valid decimal"},
          {validate: (val) => val >= -90 && val < 90, message: "your input shall be in [-90, 90)"},
        ]
      }
    },
    computed: {
      mg() {
        let s = "";
        let lon = (parseFloat(this.form.lon) + 180) / 360;
        let lat = (parseFloat(this.form.lat) + 90) / 180;

        let {char: lonCh1, rest: lon1} = iter(lon, s1);
        s += lonCh1;
        let {char: latCh1, rest: lat1} = iter(lat, s1);
        s += latCh1;

        let {char: lonCh2, rest: lon2} = iter(lon1, s2);
        s += lonCh2;
        let {char: latCh2, rest: lat2} = iter(lat1, s2);
        s += latCh2;

        let {char: lonCh3, rest: lon3} = iter(lon2, s3);
        s += lonCh3;
        let {char: latCh3, rest: lat3} = iter(lat2, s3);
        s += latCh3;

        let {char: lonCh4, rest: lon4} = iter(lon3, s4);
        s += lonCh4;
        let {char: latCh4, rest: lat4} = iter(lat3, s4);
        s += latCh4;

        let {char: lonCh5, rest: lon5} = iter(lon4, s5);
        s += lonCh5;
        let {char: latCh5, rest: lat5} = iter(lat4, s5);
        s += latCh5;

        let {char: lonCh6} = iter(lon5, s6);
        s += lonCh6;
        let {char: latCh6} = iter(lat5, s6);
        s += latCh6;
        return s;

      }
    }
  }
</script>

<style scoped>

</style>
