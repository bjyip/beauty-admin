<template>
    <div>
        <head-top></head-top>
		<section class="data_section">
			<header class="section_title">数据统计</header>
			<el-row :gutter="20" style="margin-bottom: 10px;">
                <el-col :span="5"><div class="data_list today_head"><span class="data_num head">当日数据：</span></div></el-col>
				<el-col :span="5"><div class="data_list"><span class="data_num">{{apiCount}}</span> 颜值测试</div></el-col>
				<el-col :span="4"><div class="data_list"><span class="data_num">{{userCount}}</span> 明星面对面</div></el-col>
				<el-col :span="4"><div class="data_list"><span class="data_num">{{orderCount}}</span> 纹眉神器</div></el-col>
                <el-col :span="4"><div class="data_list"><span class="data_num">{{adminCount}}</span> 抽奖游戏</div></el-col>
			</el-row>
            <el-row :gutter="20">
                <el-col :span="5"><div class="data_list all_head"><span class="data_num head">总数据：</span></div></el-col>
                <el-col :span="5">
                    <div class="data_list">
                        <span class="data_num">{{allApi}}<span class="wan" v-if="allApiCount > 10000">万</span>
                        </span> 颜值测试
                    </div>
                </el-col>
                <el-col :span="4"><div class="data_list"><span class="data_num">{{allUserCount}}</span> 明星面对面</div></el-col>
                <el-col :span="4"><div class="data_list"><span class="data_num">{{allOrderCount}}</span> 纹眉神器</div></el-col>
                <el-col :span="4"><div class="data_list"><span class="data_num">{{allAdminCount}}</span> 抽奖游戏</div></el-col>
            </el-row>
		</section>
		<tendency :sevenDate='sevenDate' :sevenDay='sevenDay'></tendency>
    </div>
</template>

<script>
	import headTop from '../components/headTop'
	import tendency from '../components/tendency' 
	import dtime from 'time-formater'
	import {apiCount, userCount, orderCount, apiAllCount, getUserCount, getOrderCount, adminDayCount, adminCount} from '@/api/getData'
    export default {
    	data(){
    		return {
    			apiCount: 12,
    			userCount: 22,
    			orderCount: 21,
                adminCount: 34,
                allApiCount: 123,
                allUserCount: 223,
                allOrderCount: 123,
                allAdminCount: 221,
    			sevenDay: [],
    			sevenDate: [[2,13,42,11,113,42,21],[22,13,42,111,21,33,11],[13,42,111,21,33,11,33],[111,21,33,11,43,21,74]],
    		}
    	},
    	components: {
    		headTop,
    		tendency,
    	},
    	mounted(){
    		this.initData();
    		for (let i = 6; i > -1; i--) {
    			const date = dtime(new Date().getTime() - 86400000*i).format('YYYY-MM-DD')
    			this.sevenDay.push(date)
    		}
    		this.getSevenData();
    	},
        computed: {
            allApi: function (){
                return this.allApiCount < 10000 ? this.allApiCount : (this.allApiCount/10000).toFixed(2)
            }
        },
    	methods: {
    		async initData(){
    			const today = dtime().format('YYYY-MM-DD')
    			// Promise.all([apiCount(today), userCount(today), orderCount(today), adminDayCount(today), apiAllCount(), getUserCount(), getOrderCount(), adminCount()])
    			// .then(res => {
    				// this.apiCount = res[0].count;
    				// this.userCount = res[1].count;
    				// this.orderCount = res[2].count;
        //             this.adminCount = res[3].count;
        //             this.allApiCount = res[4].count;
        //             this.allUserCount = res[5].count;
        //             this.allOrderCount = res[6].count;
        //             this.allAdminCount = res[7].count;
    			// }).catch(err => {
    			// 	console.log(err)
    			// })
    		},
    		async getSevenData(){
    			const apiArr = [[],[],[],[]];
    	// 		this.sevenDay.forEach(item => {
    	// 			apiArr[0].push(apiCount(item))
    	// 			apiArr[1].push(userCount(item))
    	// 			apiArr[2].push(orderCount(item))
     //                apiArr[3].push(adminDayCount(item))
    	// 		})
    	// 		const promiseArr = [...apiArr[0], ...apiArr[1], ...apiArr[2], ...apiArr[3]]
    	// 		Promise.all(promiseArr).then(res => {
    	// 			const resArr = [[],[],[],[]];
					// res.forEach((item, index) => {
					// 	if (item.status == 1) {
					// 		resArr[Math.floor(index/7)].push(item.count)
					// 	}
					// })
					// this.sevenDate = resArr;
    	// 		}).catch(err => {
    	// 			console.log(err)
    	// 		})
    		}
    	}
    }
</script>

<style lang="less">
	@import '../style/mixin';
	.data_section{
		padding: 20px;
		margin-bottom: 40px;
		.section_title{
			text-align: center;
			font-size: 30px;
			margin-bottom: 10px;
		}
		.data_list{
			text-align: center;
			font-size: 14px;
			color: #666;
            border-radius: 6px;
            background: #E5E9F2;
            .data_num{
                color: #333;
                font-size: 26px;

            }
            .head{
                border-radius: 6px;
                font-size: 24px;
                padding: 0 10px;
                color: #fff;
            }
        }
        .today_head{
            background: #FF9800;
        }
        .all_head{
            background: #20A0FF;
        }
	}
    .wan{
        .sc(16px, #333)
    }
</style>
