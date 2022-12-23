<template>
	<div class="yapilacak" :class="{yapildi:task.yapildi}">
		<div class="baslik">
			<h3 @click="showdetail=!showdetail">{{task.baslik}}</h3>
			<div class="icon">
				<router-link :to="{name:'YapilacakGuncelle',params:{id:task.id}}">
					<i class="material-icons">edit</i>
				</router-link>
				<i class="material-icons" @click="deleteTask">delete</i>
				<i class="material-icons tick" @click="toggle">done</i>
			</div>
		</div>
		<div v-if="showdetail" class="detay">
			<p>{{task.icerik}}</p>			
		</div>
	</div>
</template>
<script>
	export default{
		props:["task"],
		data(){
			return{
				showdetail:false,
				uri:"http://localhost:3000/yapilacaklar/"+this.task.id
			}
		},
		methods:{
			deleteTask(){
				fetch(this.uri,{method:'DELETE'})
				.then(()=>this.$emit('delete',this.task.id))
				.catch((err)=>console.log(err))

			},
			toggle(){
				fetch(this.uri,{
					method:'PATCH',
					headers:{'Content-Type':'application/json'},
					body:JSON.stringify({yapildi:!this.task.yapildi})
				}).then(()=>{
					this.$emit('completed',this.task.id)
				}).catch((err)=>console.log(err))
			}
		}
	}
</script>
<style>
	.yapilacak{
		margin:20px auto;
		background-color: #4b4b4b;
		padding: 10px 20px;
		border-radius: 15px;
		border:3px solid #b33939;
		color:#f7f1e3;
	}

	.yapilacak:hover{
		box-shadow: 8px 10px 10px rgba(2,2,2,0.3);
	}
	h3{
		cursor: pointer;
	}

	.baslik{
		display: flex;
		justify-content: space-between;
		align-content: center;
	}
	.baslik .icon{
		margin-top: 14px;
	}
	.material-icons{
		font-size: 25px;
		margin-left: 10px;
		color:#bbb;
		cursor: pointer;
	}
	.material-icons:hover{
		color:#2f3543
	}

	.yapilacak.yapildi{
		border:3px solid #218c74
	}

	.yapilacak.yapildi .tick{
		color:#218c74
	}
</style>