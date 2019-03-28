<template>

</template>
 
<script>
export default {
  data: function() {
    return {
      event: [
        {
          name: "กิจกรรม",
          date: "1/2/62"
        },
        {
          name: "กิจกรรม2",
          date: "1/2/62"
        },
        {
          name: "กิจกรรม3",
          date: "1/2/62"
        },
        {
          name: "กิจกรรม4",
          date: "1/2/62"
        }
      ]
    };
  }
};
</script>

<style>
.container {
  flex: 1;
  padding-left: 10px;
  padding-right: 10px;
  margin-top: 10px;
}
.loginPageHead {
  font-size: 30;
  text-align: center;
}
.HomeHead {
  margin-top: 10px;
  font-size: 18;
  text-align: left;
  padding-left: 3px;
  color: gray;
}
.HomeEvent {
  padding-left: 3px;
  padding-bottom: 3px;
}
.HomeEventTitle {
  margin-top: 10px;
  font-size: 16;
  text-align: left;
  padding-left: 3px;
}
</style>