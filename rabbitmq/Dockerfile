# Use the official RabbitMQ image with the management plugin
FROM rabbitmq:3-management

# Install curl for health checks
RUN apt-get update && \
    apt-get install -y curl && \
    rm -rf /var/lib/apt/lists/*

# Set the default user and password
ENV RABBITMQ_DEFAULT_USER=admin
ENV RABBITMQ_DEFAULT_PASS=admin123

# Expose RabbitMQ ports
EXPOSE 5672 15672

# Set the health check
HEALTHCHECK CMD curl -f http://localhost:15672/api/healthchecks/node || exit 1

# Start RabbitMQ server
CMD ["rabbitmq-server"]

