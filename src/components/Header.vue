<template>
	<v-app-bar color="deep-purple" >
		<v-toolbar-title>My Blog</v-toolbar-title>
		<v-spacer></v-spacer>
		<div class="header">
			<ul class="navbar">
				<li>
					<router-link to="/" exact>Add Blog</router-link>
				</li>
				<li>
					<router-link to="/view-blogs" exact>View Blogs</router-link>
				</li>
			</ul>
		</div>
	</v-app-bar>

</template>
<script>


export default {
	name: 'Header',
	data() {
		return {
			links: ['Home', 'Add Blog', 'View List']
		}
	}
}
</script>



<style scoped>

.header ul.navbar {
	position: relative;
	margin: 0;
	padding: 0;
}

.header ul li {
	display: inline-block;
	text-decoration: none;
	padding: 14px;
}

.header ul li a {
	width: 100%;
	text-decoration: none;
	color: #343434;
}

.header ul li a:hover {
	color: blue;
}

.router-link-active {
	color: #0000cc;
}
</style>
