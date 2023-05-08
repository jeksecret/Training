# Insights on this Section
#### 4 must have files in your project:
1. Dockerfile
2. .dockerignore
3. docker-compose.yml
4. .env
#### General tips:
- Log to STDOUT
- Use ENV variables
- Keep your app stateless

`docker build command for laravel`
```
docker build -f ./Dockerfile -t laravel-app:1.0.0 .
```
