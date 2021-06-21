<template>
  <div class="home-page">
	  <h2>Latest Posts</h2>
    <div class="articles">
      <div class="article" v-for="article of articles" :key="article">
			  <nuxt-link :to="{ name: 'slug', params: { slug: article.slug } }">
				  <div class="article-inner">
							<div class="detail">
							<h3>{{ article.title }}</h3>
							<p>{{ article.description }}</p>
						</div>
				  </div>
			  </nuxt-link>
		  </div>
    </div>
  </div>

</template>

<script>


export default {


	async asyncData({ $content, params }) {
		const articles = await $content('blog', params.slug)
			.only(['title', 'description', 'slug'])
			.sortBy('createdAt', 'desc')
			.fetch();
		return {
			articles
		}
	},

};



</script>

<style>
.home-page {
  padding: 70px 30px;



}
h2 {
    margin-bottom: 30px;
    text-align: center;
    font-family: "Verdana";
    color: black;
    font-size: 26px;

}
.articles {

  margin: 0 auto;
  max-width: 800px;
 }
.article {
  margin-bottom: 15px;
}
.article-inner {
  padding: 15px;
  background: #FFF;
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  display: flex;
}

.article-inner .detail {
  padding-left: 15px;
  padding-right: 15px;

}



h3 {
  color: #212121;
  font-size: 20px;
  text-decoration: none;
  font-family: "Verdana";
}

p {
  color: #000000;
  font-size: 18px;
  text-decoration: none;
  font-family: "Verdana";
}



footer {
  background-color: #777;
  padding: 10px;
  text-align: center;
  color: white;
}

</style>
