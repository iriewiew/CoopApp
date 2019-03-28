<template>
  <!-- login -->
  <nb-container v-if="login" style="background-color: rgb(247, 111, 77);">
    <nb-content style=" margin-top: 10%; ">
      <text>{{ruleForm}}</text>
      <text>{{Alldata}}</text>
      <nb-thumbnail class="loginLogo" large :source="logo"/>
      <nb-form style="padding-right: 4%">
        <text class="loginPageHead">ศูนย์สหกิจศึกษา มหาวิทยาลัยราชภัฏลำปาง</text>
        <text class="loginPage">COOPERATIVE EDUCATION CENTER</text>
        <nb-item floatingLabel>
          <nb-icon class="loginPageLabel" type="Feather" name="user"/>
          <nb-label class="loginPageLabel">ชื่อผู้ใช้</nb-label>
          <nb-input class="loginPageInput" v-model="ruleForm.email"/>
        </nb-item>
        <nb-item floatingLabel>
          <nb-icon class="loginPageLabel" type="Feather" name="lock"/>
          <nb-label class="loginPageLabel">รหัสผ่าน</nb-label>
          <nb-input class="loginPageInput" secureTextEntry v-model="ruleForm.pass"/>
        </nb-item>

        <nb-button class="buttonLogin" block primary :onPress="Chklogin">
          <nb-text>เข้าสู่ระบบ</nb-text>
        </nb-button>
      </nb-form>
    </nb-content>
  </nb-container>
  <!-- หน้าแรก -->
  <nb-container v-else-if="page == 1">
    <nb-header transparent span style="background-color: rgb(247, 111, 77);">
      <nb-thumbnail class="miniLogo" large :source="logo"/>
      <nb-left>
        <nb-title style="padding-top: 12%">
          <text class="pageHeader"> ยินดีต้อนรับ</text>
        </nb-title>
        <nb-text class="loginPageHead">   คุณ นิกก้าแม้ว</nb-text>
      </nb-left>
      <nb-right class="iconHeader" >
        <nb-button transparent  >
          <nb-icon style="color: white" type="AntDesign" name="qrcode"/>
        </nb-button>
      </nb-right>
    </nb-header>
    <nb-content>
      <view class="container">
        <!-- <nb-card>
          <nb-card-item header>
            <text class="PageHead">ยินดีต้อนรับ !</text>
          </nb-card-item>
          <nb-card-item>
            <nb-body>
              <nb-text>นิกก้าแม้ว</nb-text>
              <nb-text></nb-text>
            </nb-body>
          </nb-card-item>
          <nb-card-item footer></nb-card-item>
        </nb-card>-->
        <text class="HomeHead">กิจกรรมจากศูนย์สหกิจศึกษา</text>
        <view class="HomeEvent" v-for=" events in event" :key="events.name">
          <text class="HomeEventTitle">
            <nb-icon type="MaterialIcons" name="event-note" :style="{ fontSize: 32}"/>
            {{events.name}}
          </text>
          <text class="HomeEventTitle">{{events.date}}</text>
        </view>
      </view>
    </nb-content>
    <nb-footer>
      <nb-footer-tab>
        <nb-button :onPress="eventPage">
          <nb-icon type="Feather" name="clipboard"/>
          <nb-text>กิจกรรม</nb-text>
        </nb-button>
        <nb-button vertical badge>
          <nb-badge>
            <nb-text>99+</nb-text>
          </nb-badge>
          <nb-icon type="Feather" name="bell"/>
          <nb-text>แจ้งเตือน</nb-text>
        </nb-button>
      </nb-footer-tab>
    </nb-footer>
  </nb-container>
  <!-- หน้าแสดงกิจกรรม -->
  <nb-container v-else-if="page == 2">
    <nb-content style=" margin-top: 10%; ">
      <nb-button transparent dark :onPress="homePage">
        <nb-icon type="AntDesign" name="closecircleo"/>
      </nb-button>
      <text>กิจกรรม</text>
    </nb-content>
  </nb-container>
</template>
 


<script>
import { StackNavigator, DrawerNavigator } from "vue-native-router";
import Vue from "vue-native-core";
import { VueNativeBase } from "native-base";
import logo from "./assets/128x128.png";
import axios from "axios";
import VueAxios from "vue-axios";

Vue.use(VueAxios, axios);
Vue.use(VueNativeBase);

export default {
  data() {
    return {
      logo: logo,
      seen: true,
      page: 1,
      login: false,
      Alldata: "",
      ruleForm: {
        email: "",
        pass: ""
      },
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
  },
  methods: {
    Chklogin: function() {
      let apiURL = "http://coopcenter.lpru.ac.th/web/api/login";
      this.axios
        .post(apiURL, this.ruleForm)
        .then(response => {
          this.Alldata = response.data;

          // this.login = false;
        })
        .catch(err => {
          // if ((err.response.status == 404) | (err.response.status == 400)) {
          // }
        });
    },
    eventPage: function() {
      this.page = 2;
    },
    homePage: function() {
      this.page = 1;
    }
  }
};
</script>

 <style>
 .iconHeader{
   padding-top: 6%;
   margin-right: 5px;
 }
.loginLogo {
  align-items: center;
  justify-content: center;
  flex: 1;
  align-content: center;
  align-self: center;
  margin-top: 50px;
  margin-bottom: 10px;
}
.miniLogo {
  align-items: center;
  justify-content: center;
  height: 65px;
  width: 65px;
  margin-top: 15px;
  margin-left: 5px;
}
.loginPage {
  font-size: 14;
  text-align: center;
  margin-bottom: 10px;
  color: rgb(255, 255, 255);
}
.loginPageHead {
  font-size: 18;
  text-align: center;
  color: rgb(255, 255, 255);
}
.loginPageLabel {
  color: rgb(255, 255, 255);
  font-size: 14;
}
.loginPageInput {
  color: rgb(255, 255, 255);
}
.buttonLogin {
  margin-top: 40%;
  margin-left: 4%;
}
.container {
  flex: 1;
  padding-left: 10px;
  padding-right: 10px;
  margin-top: 10px;
}
.PageHead {
  font-size: 30;
  text-align: center;
}
.pageHeader {
  font-size: 30;
  text-align: center;
  color: white;
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