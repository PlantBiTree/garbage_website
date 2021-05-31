/* eslint-disable */
<template>
	<div style="background-color: #FFFFFF;">



		<el-row style="padding: 22px;">
			<el-col :span="12">

				<el-card class="box-card"  :body-style="{ padding: '0px', height: '60%'}" >
				   <img src="http://192.168.50.214:8080/video_img_url" class="image" ></img>
				</el-card>
			</el-col>
			<el-col :span="8" :offset="2">
			<img src="static/bar2.png" class="image"></img>
				<el-col :offset="5">

			<el-button type="success" round @click ="takeAPhotho()"> <i class="el-icon-camera"></i>拍照</el-button>
			<el-button type="warning" round @click ="GoToHome()"> <i cite="el-icon-lollipop"></i>返回首页</el-button>
			</el-col>
			</el-col>
		</el-row>

		<el-steps :active="3" align-center style="padding: 40px;">
		  <el-step title="步骤1" description="将待分类的垃圾放置于垃圾平台上待屏幕可以正确显示位置"></el-step>
		  <el-step title="步骤2" description="点击屏幕上方的拍照按钮,等待机器进行垃圾识别"></el-step>
		  <el-step title="步骤3" description="机器识别成功,等待打开相应的垃圾桶"></el-step>
		</el-steps>




	</div>

</template>

<script>
	var self
export default {
  data () {
    return {
      src: 'https://likecy.oss-cn-beijing.aliyuncs.com/0194a25dcd1b46a8012053c074fa37.jpg@2o_1574846777533.jpg'
    }
  },
	  created: function () {
		  self = this
  },
	  methods: {
	    GoToResult () {
				  this.$router.push('./result')
	    },
	    GoToHome () {
				  this.$router.push('./')
	    },
		  takeAPhotho () {
				 this.$http.get('http://192.168.50.214:8080/shut_photho', { // 还可以直接把参数拼接在url后边
    			}).then(function (res) {
					  self.$message({
          message: res.data,
          type: 'success'
					  })
				 self.deltailDataFromServers(res.data)
				 console.log(res)
    			}).catch(function (error) {
        		console.log(error)
    		})
	    },
		  deltailDataFromServers (data) {
	      var result = data.split('/')
		  switch (result[0]) {
				  case '可回收物':
				  		 self.$router.push({name: 'result',
            params: {
					 	channel: 0
					 }})
				  break
			  case '其他垃圾':
				  	 self.$router.push({name: 'result',
            params: {
					 	channel: 1
					 }})
				  break
			  case '厨余垃圾':
				  	 self.$router.push({name: 'result',
            params: {
					 	channel: 2
					 }})
				  break
			  case '有害垃圾':
				  	 self.$router.push({name: 'result',
            params: {
					 	channel: 3
					 }})
				  break
		  }
		  }
	}
}
</script>

<style>
	.image {
	    width: 50%;
		height: 60%;
	  }

</style>
