https://brainsandbeards.com/blog/advanced-redux-patterns-normalisation

https://www.youtube.com/watch?v=aJxcVidE0I0


Normalisation
The term normalisation comes from the database world. 
It refers to transforming the schema of a database to remove redundant information. 
Also, redundant information means the same data that is stored in more than one place.



Performance
Another reason to go for a normalised state in Redux is performance. If you have deeply nested structures, it’s difficult to traverse them. It’s much easier to find your data if you have it all filed by their ID in a dictionary / hash / map structure.

Imagine the performance of finding an article by its ID in a big array of articles (you’d have to go through the whole collection and check IDs along the way until you find it) compared to finding it in a dictionary structure where you can just fetch it directly by the ID.



Array Based Storage :

state = {
	posts = [post, post, post, post]
}

Object Based Storage :

state = {
	posts:{
		101: {id: 101, name:"post for 101", .....},
		102: {id: 102, name:"post for 102", .....},
		103: {id: 103, name:"post for 103", .....},
		109: {id: 109, name:"post for 109", .....},
	}
}

Reading a Record:
Array Based:
let id = 109;
state.posts.find(post => post.id === id);

Object Based:

state.posts[id];

Update: 
Array Based:
const newPost = {id: 45}
const newwState =  state.posts.filter(post => post.id !==id);
return [...newwState, newwPost];
Object Based:
const newPost = {id: 45}
return {...state, [newPost.id]: newPost};

Delete: 
const deletedId = 45;
state.posts.filter(post => post.id !==deletedId);

Object Based:
const deletedId = 45;
retun _.omit(state, deletedId);







Each type of data gets its own table. Each table is an object.Item id is the key and the value is the item.

{
	posts: { ... },
	comments: { ... },
	users: { ... }
}

{
	posts: {
		entities: {
			post1: {},
			post2: {}
		}
	},
	...
	

}

Item order is stored in an array containing the item ids.
ids as an array
entities as dictonary

{
	posts: {
		entities: {
			post1: {},
			post2: {}
		},
		ids: ['post1', 'post2']
		
	},
}
Related items are referenced by id.

{
	posts: {
		entities: {
			post1: { auther: 'user1' }
		}
	},
	users: {
		entities: {
			user1: { name: 'User one' }
		}
	}
}

library to normalize the data:
normalizr:
https://www.npmjs.com/package/normalizr

