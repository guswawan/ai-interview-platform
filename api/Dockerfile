# Use an official Ruby runtime as a parent image
FROM ruby:3.3.2-slim-bullseye

# Set working directory
WORKDIR /app

# Set frontend non-interactive to prevent hanging during build
ENV DEBIAN_FRONTEND=noninteractive

# Install PostgreSQL client libraries, NodeJS and other build essentials
RUN apt-get update -y && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends build-essential libpq-dev nodejs && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean

# Install Bundler
RUN gem install bundler:2.5.11

# Copy Gemfile and Gemfile.lock
COPY Gemfile Gemfile.lock ./ 

# Install dependencies
RUN bundle install --jobs=$(nproc) --without development test

# Copy the rest of the application code
COPY . .

# Expose port 3000 to the Docker host
EXPOSE 3000

# Command to run the Rails server
CMD ["bundle", "exec", "rails", "s", "-b", "0.0.0.0"]
