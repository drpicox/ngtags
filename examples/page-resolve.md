Page Resolvers
===============

Example of a page that requires to resolve some data before with promises.


```html
<angular-page name="/posts/:postId">
    <template>
        <h1>{{vm.post.title}}</h1>
        <div ng-bind-html="vm.post.content"></div>
        <hr>
        <ul><li ng-repeat="related in relateds">{{related}}</li></ul>
    </template>
    <resolve>
        <script name="post" params="postId" inject="postsService">
            return postsService.load(postId);
        </script>
        <script name="relateds" params="postId" inject="relatedsService">
            return relatedsService.find(postId);
        </script>
    </resolve>
    <script>
        this.post = post;
        this.relateds = relateds;
    </script>
</angular-page>
```

Generated code:

```javascript
/*
	Route /posts/:postId
	Controller PostsPostIdController as vm.

*/
;(function(angular) {
	'use strict';

	angular
		.module('ntagExamples')
		.config(PostsPostIdRoute);
	

	PostsPostIdRoute.$inject = ['$routeProvider'];
	function PostsPostIdRoute  ( $routeProvider ) {

		$routeProvider.when('/posts/:postId', {
			controller: PostsPostIdController,
			controllerAs: 'vm',
			resolve: {
				post: postResolve,
				relateds: relatedsResolve,
			},
			template: '\n        <h1>{{vm.post.title}}</h1>\n        <div ng-bind-html=\"vm.post.content\"></div>\n        <hr>\n        <ul><li ng-repeat=\"related in relateds\">{{related}}</li></ul>\n    ',
		});

	}

	
	PostsPostIdController.$inject = ['post','relateds'];
	function PostsPostIdController  ( post , relateds ) {
		
        this.post = post;
        this.relateds = relateds;
    
	}
	

	
	postResolve.$inject = ['postsService','$route'];
	function postResolve  ( postsService , $route ) {
		var postId = $route.current.params.postId;
				
		return postsService.load(postId);
		
	}

	
	relatedsResolve.$inject = ['relatedsService','$route'];
	function relatedsResolve  ( relatedsService , $route ) {
		var postId = $route.current.params.postId;
				
		return relatedsService.find(postId);
		
	}

})(angular);
```