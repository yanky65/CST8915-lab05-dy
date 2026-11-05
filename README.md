# CST8915 Lab 5 - Containerizing the Algonquin Pet Store

Student: David Yin

## Demo Video

REPLACE_WITH_YOUTUBE_LINK

## Service Repositories

- Order: https://github.com/yanky65/order-service-L4
- Product: https://github.com/yanky65/product-service-python-L4
- Frontend: https://github.com/yanky65/store-front-L4

## Docker Hub Images

- https://hub.docker.com/r/noobstang/order-service
- https://hub.docker.com/r/noobstang/product-service
- https://hub.docker.com/r/noobstang/store-front

## Implementation

The Product Service uses Python and Flask.

The application runs locally using Docker Desktop with Linux containers.
Docker Compose runs RabbitMQ, order-service, product-service, and store-front.

The Store Front image contains these API base URLs:
- Order API: http://localhost:3000
- Product API: http://localhost:3030

The storefront is available at http://localhost:8080.

RabbitMQ stores orders in the durable order_queue queue.
A named volume preserves broker data when containers are recreated.

## Run the Published Images

1. Clone this repository.
2. Copy .env.example to .env.
3. Replace the placeholder broker password and Docker Hub username.
4. Run docker compose pull.
5. Run docker compose up -d --wait.
6. Open http://localhost:8080.

The Compose configuration runs published Docker Hub images without local source builds.

The frontend image targets APIs on localhost. A deployment using different API
addresses requires rebuilding and republishing the frontend image.

## Verify

- Open http://localhost:3030/products to check the catalog.
- Place an order through the storefront.
- Run docker compose exec rabbitmq rabbitmqctl list_queues name durable messages.
- Confirm order_queue is durable and its message count increases.
