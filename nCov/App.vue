<script>
	import pageAnimation from './components/page-animation'
	export default {
		onLaunch: function() {
			// console.log('App Launch')
		},
		onShow: function() {
			// console.log('App Show')
		},
		onHide: function() {
			// console.log('App Hide')
		},
		mixins: [pageAnimation]
	}
</script>

<style>
	/* color-ui */
	@import "colorui/main.css";
	@import "colorui/icon.css";

	/*头部肺炎图 */
	.header {
		color: #fff;
		position: relative;
		background-size: cover;
		background-position: 50%;
		background-repeat: no-repeat;
		padding: 0;
		height: 220px;
		margin-bottom: -380rpx;
		z-index: 1;
		background-color: #10aeb5;
		background-image: url(./static/bg-header.jpg);
	}
</style>
