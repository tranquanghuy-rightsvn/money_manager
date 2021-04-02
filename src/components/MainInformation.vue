<template>
	<div> 
		<ul class="list">
			<li v-for="item in info.slice().reverse()" :key="item.index" class="spending" :class="{income: item.type === 1}"  >
				<div class="list-item__left parent">
					<span>{{item.type === 0 ? "-" : "+"}}{{item.money}}$ </span> : {{item.content}}
					<v-ons-icon icon="fa-pencil"> </v-ons-icon>
				</div>
			</li>
		</ul>
	</div>
</template>

<script>
export default {
  name: 'MainInformation',
  props: {
		info: {
			type: Array
		}
  }
}
</script>

<style scoped>
	div{
		text-align: center;
	}
	div {
		padding-top: 20px;
		padding-bottom: 20px;
	}
	.income span{
		color: green !important;
	}
	.spending span{
		color: red;
	}
	li div{
		padding-left: 10px;
	}
	v-ons-icon{
		margin-left: 5px;
	}
	
</style>