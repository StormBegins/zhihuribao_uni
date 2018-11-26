

<template>
	<div v-html="datas" ref="link">
		{{datas}}
	</div>
</template>

<script>
	export default {
		mounted(){
			this.axios({
				method:'get',
				url:'/api/api/4/news/latest'
			})
			.then(response => {
				this.dailyNewspaper(response);
			})
			.catch(error => {
				console.log(error)
			});
		},		
		data: function() {
			return {
				datas:null,
				dailyPhoto:null,
				dailyHeadline:null,
				dailyContainer:null
			}
		},
		methods: {
			dailyNewspaper(datas){
				console.log();
				this.dailyPhoto = "<div style='float:right; width:25%'><img src="+datas.data.stories[0].images[0]+" style='width:100px; height:100px;' /></div>";
				this.dailyHeadline = "<div style='float:left; width:65%; font-size:20px; font-weight:600;'>"+datas.data.stories[0].title+"</div>";
				this.dailyContainer = "<div class='a' style='float:left; width:96%; background-color:gray; padding:10px; margin:10px;'>"+this.dailyHeadline+this.dailyPhoto+"</div>";
				this.datas = this.dailyContainer;
				for (var i = 1; i < datas.data.stories.length; i++) {
					id = datas.data.stories[i].id;
					this.dailyPhoto = "<div style='float:right; width:25%'><img src="+datas.data.stories[i].images[0]+" style='width:100px; height:100px;' /></div>";
					this.dailyHeadline = "<div style='float:left; width:65%; font-size:20px; font-weight:600;'>"+datas.data.stories[i].title+"</div>";
					this.dailyContainer = "<div class='a' style='float:left; width:96%; background-color:gray; padding:10px; margin:10px;'>"+this.dailyHeadline+this.dailyPhoto+"</div>";
					this.datas += this.dailyContainer;
				}
			}
		}
	}
</script>
