<template>
	<div class="group">
		<button v-bind:class="{'white': whites.indexOf(n) > -1,'black': blacks.indexOf(n) > -1}" v-for="n in 12" v-bind:style="{left: calcLeft(n) + '%'}" data-note="{start + n}" v-on:click="play(n)" ><span v-show="n===0">C</span></button>
	</div>
</template>
<script>
 import {notes} from '../notes.js';
 const prefix = 'data:audio/mpeg;base64,';
 const base = 2;
 const keys = 12;
 export default {
 	props: ['group'],
 	data() {
 		return {
 			blacks: [1,3,6,8,10],
 			whites: [2,4,5,7,9,11,12]
 		}
 	},
 	computed: {
 		start: function(){
 			return this.group * keys;
 		}
 	},
 	methods:{
 		play(index) {
 			var audio = new Audio(prefix + notes[index + base]);
 			audio.play();
 		//	console.log(notes[index+base]);
 		},
 		calcLeft(index) {
 			var unit = 14.29;
 			var i = this.blacks.indexOf(index);
 			if(i < 2){
 				return unit*(0.75 + i);
 			}
 			return unit*(1.75 + i);
 		},
 		click(index){

 		}
 	}
 }
</script>
<style lang="less">
.group {
	font-size: 0;
	position: relative;
	display: flex;
	flex-grow: 1;//定义flex item的拉伸因子
}
button {
	width: 14.29%;
	flex: 1;
	height: 300px;
	display: inline-block;
	border: 1px solid #ccc;
	outline: 0;
	padding: 0;
	box-sizing: border-box;//宽度高度涉及到外边框
}
button > span {
	position: absolute;
	bottom: 10px;
}
.white:active,
.white.active {
	background: #ececec;
}
.white {
	background: #fff;
}
.black {
	background: #000;
	border-color: #000;
	height: 150px;
	width: 7.15%;
	position: absolute;
}
</style>