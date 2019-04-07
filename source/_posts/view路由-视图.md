---
title: vue路由/视图
date: 2019-04-07 12:41:58
tags: （V）vue路由/视图
---

### 1、命名路由
	const router = new VueRouter({
	  routes: [
	    {
	      path: '/user/:userId',
	      name: 'user',		// 给路由命名
	      component: User
	    }
	  ]
	})
	// 就是给route一个名字

### 2、嵌套路由

	const router = new VueRouter({
	  routes: [
	    { path: '/user/:id', component: User,
	      children: [
	        {
	          // 当 /user/:id/profile 匹配成功，
	          // UserProfile 会被渲染在 User 的 <router-view> 中
	          path: 'profile',
	          component: UserProfile
	        },
	        {
	          // 当 /user/:id/posts 匹配成功
	          // UserPosts 会被渲染在 User 的 <router-view> 中
	          path: 'posts',
	          component: UserPosts
	        }
	      ]
	    }
	  ]
	})
	// 就是路由下面有子路由children: [path:...]

#### 嵌套路由和命名路由不是对立的概念

### 3、命名视图

	// 一个路由下---多个视图（多个组件）
	// js
	const router = new VueRouter({
	  routes: [
	    {
	      path: '/',
	      components: {
	        default: Foo,	// 给3个视图命名
	        a: Bar,
	        b: Baz
	      }
	    }
	  ]
	})
	// html
	// 如果 router-view 没有设置名字，那么默认为 default
	<router-view class="view one"></router-view>
	<router-view class="view two" name="a"></router-view>
	<router-view class="view three" name="b"></router-view>

#### 3.1 嵌套命名视图

嵌套--多级，并且有命名

	{
	  path: '/settings',
	  component: UserSettings,	//一级路由，一对一（未命名）
	  children: [{
	    path: 'emails',
	    component: UserEmailsSubscriptions
	  }, {
	    path: 'profile',
	    components: {			//二级路由，一对多（2个视图命名了）
	      default: UserProfile,
	      helper: UserProfilePreview
	    }
	  }]
	}