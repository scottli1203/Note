# Note
SELECT * FROM user_token ut 
JOIN user_token ut2 ON ut.user_id = ut2.user_id
AND ut2.token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImxpY2h1YW53ZWkiLCJyb2xlIjoxLCJpYXQiOjE1MDM5MzEzMDAsImV4cCI6MTUwNDAxNzcwMH0.D1qg6FzZYEnLXhKIYNuB6EBQu31-ffV8xdTpU1IFtqs'
ORDER BY ut2.created_time DESC limit 1


CREATE TABLE `user_token` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) NOT NULL,
  `email` varchar(100) NOT NULL,
  `token` varchar(200) NOT NULL,
  `created_time` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `updated_time` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

let sql = `INSERT INTO user_token(user_id,email,token) VALUES(${userId},'${email}','${token}')`

          model.sequelize.query(sql).then((result) => {
            console.log(result)
          })


import React from 'react'
import { render } from 'react-dom'
import { Router, Route, browserHistory, IndexRoute } from 'react-router'
// import App from './modules/App'
// import About from './modules/About'
// import Repos from './modules/Repos'
// import Repo from './modules/Repo'
// import Home from './modules/Home'

// render((
//   <Router history={hashHistory}>
//     <Route path="/" component={App}>
//       <IndexRoute component={Home}/>
//       <Route path="/repos" component={Repos}>
//         <Route path="/repos/:userName/:repoName" component={Repo}/>
//       </Route>
//       <Route path="/about" component={About}/>
//     </Route>
//   </Router>
// ), document.getElementById('app'))

const rootRoute = {
    path: '/',
    indexRoute: {
        getComponent(nextState, cb) {
            require.ensure([], (require) => {
                cb(null, require('./modules/Home').default)
            }, 'HomePage')
        },
    },
    getComponent(nextState, cb) {
        require.ensure([], (require) => {
            cb(null, require('./modules/App').default)
        }, 'App')
    },
    childRoutes: [
        {
            path:'about',
            getComponent(nextState, cb) {
                require.ensure([], (require) => {
                    cb(null, require('./modules/About').default)
                }, 'About')
            }
        },
        {
            path:'repos',
            getComponent(nextState, cb) {
                require.ensure([], (require) => {
                    cb(null, require('./modules/Repos').default)
                }, 'Repos')
            }
        },
        {
            path:'reactjs',
            getComponent(nextState, cb) {
                require.ensure([], (require) => {
                    cb(null, require('./modules/Repo').default)
                }, 'Repo')
            },
        }
    ]
}

render(
        <Router
            history={browserHistory}
            routes={rootRoute}
        />
    , document.getElementById('app')
);
