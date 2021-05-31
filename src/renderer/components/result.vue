<template>


	<el-container>
	  <el-header style="padding: 40px;"><div class="text-olive text-xxl">垃圾识别结果</div></el-header>
	  <el-main style="background-color: #FFFFFF;" >


		  <el-row>
		    <el-col :span="4"  :offset="2" v-for="(item,index) in ClassList"  :key="index" >
				<div :class="index==channel?'divcss5':''">
<!--				<div class="divcss5">-->
					<el-card :body-style="{ padding: '0px' }">
		        <img :src="item.url" class="image">
		      </el-card>
				</div>

		    </el-col>

		  </el-row>


		  <el-row style="padding-top: 3.125rem;">
			  <el-alert
			      title="垃圾分类的好处和意义有哪些"
			      type="success"
			      description="1、减少环境污染
                                 通过填埋或者堆放处理垃圾，
                                 也难以杜绝有害物质渗透，这些有害物质随着地球的循环进入到整个生态圈中，
                                 污染水源和土地，通过植物或者动物，影响人们的身体健康。
                               2、节省土地资源
                                  垃圾填埋占用土地资源，使土地受到严重侵蚀。
                                  将垃圾分类，去掉可以回收的、不易降解的物质，减少垃圾数量达60%以上。
                               3、再生资源的利用垃圾的产生是源于人们没有利用好资源。在垃圾处理之前，通过垃圾分类回收，
                                  就可以将垃圾变废为宝。
                               4、提高民众价值观念
                                  垃圾分类能够使得民众学会节约资源、利用资源，
                                  养成良好的生活习惯，提高个人最终的素质素养。"
				  :closable="false">
			    </el-alert>
		  </el-row>


		  <el-row style="padding: 70px;" >
			<el-col :span="18"  :offset="7" >
				<el-button type="danger" round @click="OpenMotor()" >再次打开垃圾桶</el-button>
				<el-button type="success" round @click ="GoToPredict()">再次识别</el-button>
				<el-button type="primary" round @click="GoToHome()">返回首页</el-button>
			</el-col>
		  </el-row>




	  </el-main>
	</el-container>




</template>

<script>
	var self
export default {
	  data () {
	    return {
	      src: 'https://cube.elemecdn.com/6/94/4d3ea53c084bad6931a56d5158a48jpeg.jpeg',
	      channel: '',
	      ClassList: [{
	      	url: 'static/image/1.png'
	      }, {
	      	url: 'static/image/2.png'
	      }, {
	      	url: 'static/image/3.png'
	      }, {
	      	url: 'static/image/4.png'
	      }]
	    }
	  },
	  created: function () {
    console.log('created 创建完毕状态*********************》')
	    this.channel = this.$route.params.channel
	    this.OpenMotor()
	    self = this
  },
	  methods: {
	    GoToPredict () {
					  this.$router.push('./predict')
	    },
	    GoToHome () {
					  this.$router.push('./')
	    },
	    OpenMotor () {
	      var channel = this.channel
	      console.log('开始舵机')
	      this.$notify({
         		 title: '垃圾桶通知',
          		 message: '垃圾桶即将打开',
				 type: 'success'
       			 })
			 this.$http.get('http://192.168.50.214:8080/open_motor?channel=' + channel, { // 还可以直接把参数拼接在url后边
    			}).then(function (res) {
					 // alert(res.data);
					 self.$notify({
         		    title: '垃圾桶通知',
          		    message: '垃圾桶已经关闭'

       			    })
				 console.log(res)
    			}).catch(function (error) {
        		console.log(error)
    		})
    }
	  }
	}
</script>

<style>
	.image {
	    width: 100%;
	    display: block;
	  }
	.divcss5{ border:solid 10px #e54d42;
	}
</style>
