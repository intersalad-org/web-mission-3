# Миссия 3

https://www.loom.com/share/661f6291b2894d7b9ebc029ea305b989?sid=fb9b01b4-773b-4cdf-9ff6-4161d713ecc8

SQL запросы

1. Получить список юзернеймов пользователей

SELECT username from users

2. Получить кол-во отправленных сообщений каждым пользователем:
 
SELECT
  m."from",
  u."username",
  COUNT(m.id) AS number_of_sent_messages
FROM
  messages m
  JOIN users u ON m."from" = u.id
GROUP BY
  m."from",
  u."username";


3. Получить пользователя с самым большим кол-вом полученных сообщений и само количество
    
SELECT
  u.username from users u
JOIN (select id, count(*) as message_count FROM messages group by id) m on u.id = m.id
ORDER BY message_count desc limit 1;
  
    
4. Получить среднее кол-во сообщений, отправленное каждым пользователем

   SELECT
  AVG(message_count) AS average
FROM
  (
    SELECT
      m."from",
      u."username",
      COUNT(m.id) AS message_count
    FROM
      messages m
      JOIN users u ON m."from" = u.id
    GROUP BY
      m."from",
      u."username"
      ) AS message_counts;
