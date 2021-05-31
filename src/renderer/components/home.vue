<template>
  <div style="background-color: #FFFFFF">


<el-carousel :interval="4000" type="card" height="280px">
    <el-carousel-item v-for="(index,item) in BarImgList" :key ="item">
    <el-image :src="index.url"></el-image>
    </el-carousel-item>
</el-carousel>

	<el-card :body-style="{ padding: '10px', margin:'10px' }" >
		<el-row>
	  <el-col :span="6"  v-for="(item,o) in menubarList" :key="o" :offset="o!=0?2:1" >
	    <el-card :body-style="{ padding: '0px' }" >
	      <img :src="item.img" class="image"  @click="GoToWhere(item.dir)">
			<div class="text3D">
           <h2>{{item.name}}</h2>
     	 </div>
		</el-card>
	  </el-col>
</el-row>
	</el-card>


  </div>
</template>


<script>
export default {
  data () {
    return {
      BarImgList: [{
        url: 'https://likecy.oss-cn-beijing.aliyuncs.com/bar2_1575171458767.png'
      },
      {
        url: 'https://likecy.oss-cn-beijing.aliyuncs.com/bar1_1575171455747.png'
      },
      {
        url: 'https://likecy.oss-cn-beijing.aliyuncs.com/bar3_1575172252487.png'
      }
      ],
      menubarList: [{
        name: '垃圾分类识别',
        img: 'static/home2.png',
        dir: 'predict'
      }, {
        name: '识别竞猜',
        img: 'static/home1.jpg',
        dir: 'predict'
      }, {
        name: '更多...',
        img: 'static/home1.jpg',
        dir: 'predict'
      }
      ]

    }
  },
  methods: {
	  GoToWhere (dir) {
		  this.$router.push(dir)
	  }
  }
}
</script>


<style>
	  .bottom {
	    margin-top: 13px;
	    line-height: 12px;

		  /*ssss*/
	  }

	  .button {
	    padding: 0;
	    float: right;
	  }

	  .image {
	    width: 100%;
	    display: block;
	  }

	  .clearfix:before,
	  .clearfix:after {
	      display: table;
	      content: "";
	  }

	  .clearfix:after {
	      clear: both
	  }

	.text3D h2 {
				text-align: center;
				color: #4fcc1d; text-shadow: 1px 1px 0px #4fcc1d;
	}
</style>
