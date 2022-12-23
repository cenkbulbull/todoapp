<template>
	<div class="home">
		<NavbarFilter @filterStatus="activeTab=$event" :activeTab="activeTab"/>
		<div v-if="tasks.length">
			<div v-for="item in filterTasks" :key="item.id">
				<Yapilacak :task="item" @delete="handleDelete" @completed="handleCompleted"/>
			</div>
		</div>
		<div v-else>
			<p>Yükleniyor!!</p>
		</div>
	</div>
</template>
<script>
	import Yapilacak from "../components/Yapilacak"
	import NavbarFilter from "../components/NavbarFilter"
	export default{
		name:"Home",
		components:{
			Yapilacak,
			NavbarFilter
		},
		data(){
			return{
				tasks:[],
				activeTab:"all"
			}
		},
		mounted(){
			fetch("http://localhost:3000/yapilacaklar")
			.then((res)=>res.json())
			.then((data)=>this.tasks=data)
			.catch((err)=>console.log(err))
		},
		methods:{
			handleDelete(id){
				this.tasks=this.tasks.filter(yap=>{
					return yap.id!==id
				})
			},
			handleCompleted(id){
				let yap=this.tasks.find(task=>{
					return task.id==id
				});

				yap.yapildi=!yap.yapildi
			}
		},
		computed:{
			filterTasks(){
				if(this.activeTab==="completed"){
					return this.tasks.filter(task=>task.yapildi)
				}
				if(this.activeTab==="continues"){
					return this.tasks.filter(task=>!task.yapildi)
				}
				else{
					return this.tasks
				}
			}
		}
	}
</script>
<style>
	
</style>