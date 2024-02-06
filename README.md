# database_sharding
## Description
This project implements a simulated URL shortening service for the purpose of database sharding experiments. Sharding is a technique for dividing data into multiple database servers to improve database scalability and performance.

## POST request
<p align="center">
  <img width="736" alt="image" src="https://github.com/katsurada1/database_sharding/assets/91961057/b383a841-f21c-4ef3-a1e4-2956ca350f97">
</p>

Requests are processed in the following order.
1. When a POST request is received, the URL in the request is hashed using hashing crypt.
2. The first 5 characters of the hash value are used as the URL ID, and HashRing is used to determine the server name of the database to store the data (5432, 5433, 5434 in this case) based on this URL ID.
3. The actual server name is stored in a table of the form id, URL, URL ID that corresponds to the server name.

## GET request
<p align="center">
  <img width="488" alt="image" src="https://github.com/katsurada1/database_sharding/assets/91961057/3e0cbe22-224a-4f07-8001-fed23fb76774">
</p>

Requests are processed in the following order.
1. When a GET request is received, use the shortened URL ID in the request to determine which database has the information by HashRing.
2. It retrieves the original, unshortened URL from that database and returns the response to the client.

## Results of experiment
The following results show that the POST request actually saves the shortened URL ID information and uses it to retrieve the original, original URL.
### POST
<p align="center">
  <img width="558" alt="image" src="https://github.com/katsurada1/database_sharding/assets/91961057/56b7edb2-dbcd-4a2f-bdf4-4b7046af6163">
</p>

### GET
<p align="center">
  <img width="719" alt="image" src="https://github.com/katsurada1/database_sharding/assets/91961057/7fdee758-0f85-47ff-98eb-c02dd2cb22d3">
</p>

The following results also show that data storage is performed for various databases and that sharding is successful.
<p align="center">
  <img width="560" alt="image" src="https://github.com/katsurada1/database_sharding/assets/91961057/d8d64e0b-8bbb-422d-a698-c3663730a1d3">
</p>



