<template>
	<view style="background-color: #ffffff;">
		<z-nav-bar title="申请服务">
			<view class="preview" slot="right" @click="savework">
				<text style="font-size: 20rpx;" v-if="addtext">{{ addtext }}</text>
			</view>
		</z-nav-bar>
		<view class="u-demo-block">
			<view class="u-demo-block__content">
				<u-cell-group :border="true" class="message" display="flex">
				<u-cell @click="showNameModal" titleStyle="font-size: 14px" size="large" title="服务人员" :isLink="true">
					<text slot="value" class="u-slot-value">{{ name }}</text>
				</u-cell>
				<u-cell @click="selectDoctor" size="large" titleStyle="font-size: 14px" title="会员" :isLink="true">
					<text slot="value" class="u-slot-value">{{ didName }}</text>
				</u-cell>
			</u-cell-group>
			<u-gap height="10"></u-gap>
			<u-cell-group :border="false" class="message">
                <u-cell @click="showdate = true" class="message" titleStyle="font-size: 14px" size="large" title="日期"
					:value="date" :isLink="true">
					<text slot="value" class="u-slot-value">{{ date }}</text>
				</u-cell>
			</u-cell-group>
			</view>

            <view class="u-demo-block uni-flex uni-row service" v-for="item in dataList">
                 <!-- 6、日期 -->
                <view class="flex-item date-body">
                    <text class="cate-text">开始日期</text>
                    <view style="height: 20rpx"></view>
                    <view class="picker" @click="showCreateTime = true">
                        <uni-datetime-picker class="time-picker" :show-icon="true" :border="false"
                            v-model="item.start_time" :clearIcon="false" />
                        <uni-icons type="forward" size="15"></uni-icons>
                    </view>
                </view>	
                <view class="flex-item date-body">
                    <text class="cate-text">结束日期</text>
                    <view style="height: 20rpx"></view>
                    <view class="picker" @click="showEndTime = true">
                        <uni-datetime-picker class="time-picker" :show-icon="true" :border="false"
                            v-model="item.end_time" :clearIcon="false" />
                        <uni-icons type="forward" size="15"></uni-icons>
                    </view>
                </view>
                <u-textarea :placeholder="placeholder2" style="background-color: #f5f2 5f5;margin: 20rpx 0"
							border="false" v-model="item.content"></u-textarea>
            </view>
            
            
            <u-datetime-picker :show="showdate" v-model="chooseDate" :min-date="new Date().getTime()"
			:max-date="new Date('2070/12/31').getTime()" mode="date" closeOnClickOverlay @confirm="change = true"
			@cancel="showdate = false" @close="() => (showdate = false)"></u-datetime-picker>
		</view>
		<!-- <z-navigation></z-navigation> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
                showdate:false,
                showCreateTime:false,
                showEndTime:false,
                change: false,
				addtext:'提交',
                placeholder2:'请输入工单内容',
                chooseDate: Number(new Date()),
				count: 5,
				value: 2,
				albumWidth: 200,
				datetime: '2023-02-02 20:20',
				commentList:[],
				did:" ",
                name:'',
                didName:'',
                date: '',
                dataList:[{
                    start_time: this.formatDate(new Date()),
                    end_time: this.formatDate(new Date()),
                    save_id:0,
                    content:''
                },[],[]],
                filteredArray:[],
			}
		},
		onLoad: function () {
            this.getwork()
			this.did = uni.getStorageSync('did');
            this.didName = uni.getStorageSync('didName');
			console.log('did',this.did);
            if(localStorage.getItem('data')){
                this.data = localStorage.getItem('data')
            }
            if(localStorage.getItem('date')){
                this.date = localStorage.getItem('date')
            }
		},
		methods: {
            formatDate(date) {
			var y = date.getFullYear();  
                var m = date.getMonth() + 1;  
                m = m < 10 ? ('0' + m) : m;  
                var d = date.getDate();  
                d = d < 10 ? ('0' + d) : d;  
                var h = date.getHours();  
                h=h < 10 ? ('0' + h) : h;  
                var minute = date.getMinutes();  
                minute = minute < 10 ? ('0' + minute) : minute;  
                var second=date.getSeconds();  
                second=second < 10 ? ('0' + second) : second;  
                return y + '-' + m + '-' + d+' '+h+':'+minute+':'+second;  
		},
            confirmdata(){
                const timestamp = this.chooseDate
				const date = new Date(timestamp)
				const year = date.getFullYear()
				const month = String(date.getMonth() + 1).padStart(2, '0') // 注意月份从 0 开始计数，需要加 1，并且需要补齐位数
				const day = String(date.getDate()).padStart(2, '0') // 注意日期需要补齐位数
				this.date = `${year}-${month}-${day}`
				this.showdate = false
                this.change = false
            },
			getwork(){
				this.$http.post('/user/info',{
                    id:uni.getStorageSync('userInfo')
				}).then((res)=>{
					console.log('res',res);
                    this.name = res.data.fullname
					// this.commentList = res.data.data
				})
			},
            savework(){
                this.dataList.forEach(element => {
                    element.save_id = 0
                    if(element.content!=null && element.content!='')this.filteredArray.push(element);
                });
                if(this.filteredArray.length==0){
                    uni.showToast({
                            title: '输入工单内容',
                            icon:'none',
                            duration:2000
                        })
                }
                this.$http.post('/work/create',{
                    uid: this.did,
                    did: uni.getStorageSync('userInfo'),
                    data:this.filteredArray,
                    date:this.date,
                }).then((res)=>{
                    console.log(res);
                    if(res.message=='提交成功'){
                        uni.showToast({
                            title: '提交成功',
                            icon:'success',
                            duration:2000
                        })
                    }else{
                        uni.showToast({
                            title: '提交失败',
                            icon:'none',
                            duration:2000
                        })
                    }
                
                })
                    localStorage.setItem('',this.data)
                    localStorage.setItem('',this.date)
                    localStorage.setItem('',this.did)
            },
			selectDoctor(){
                let index = '服务人员'
                // localStorage.setItem('data',this.data)
                localStorage.setItem('date',this.date)
                localStorage.setItem('did',this.did)
				uni.navigateTo({
			    	url:'/pages/message/addressBook?title=' + index
			  })
			}
		},
        watch: {
        change: function (newVal, oldVal) {
            // 当 this.chooseDate 发生变化时，将会触发这个函数
            console.log('change 变化啦！新值为：', newVal);
            console.log('旧值为：', oldVal);
            if (this.change) this.confirmdata()
            // 在这里可以执行其他逻辑或操作，根据新的值做出相应的处理
        }
    }
	}
</script>

<style lang="scss">
	@import '@/style/mixin.scss';

	.message {
		background-color: #ffffff;
	}

	.u-slot-value {
		color: gray;
		font-size: 14px;
	}

	.form_but {
		background-color: rgb(32, 198, 162);
		color: #ffffff;
		border-radius: 50upx;
	}
    .date-body {

        display: flex;
        flex-direction: row;
        align-items: center;
        .cate-text {
            flex: 1;
        }
        background-color: white;
        // padding: 30rpx;
        // margin-bottom: 100rpx;


        .date {
            margin-right: 25rpx;
        }

        .picker {
            display: flex;
            align-items: center;
            justify-content: space-between;
            position: relative;
            // width: 50%;
            // max-width: 200px;


            .time-picker {
                margin-right: 220rpx;
            }
        }
    }
    .service{
        margin-top: 20px;
        margin-bottom: 20px;
    }

</style>