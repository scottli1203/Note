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
