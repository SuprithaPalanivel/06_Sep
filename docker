FROM node:18 as build 
WORKDIR /app 
COPY package*.json ./ 
RUN npm install 
COPY . . 
RUN npm run build 
  
# Stage 2: Create a minimal runtime image 
FROM nginx:alpine 
WORKDIR /usr/share/nginx/html 
# Copy only the build artifacts from the 'build' stage 
COPY --from=build /app/build . 
  
# Expose port 80 
EXPOSE 80 
  
# Start Nginx 
CMD ["nginx", "-g", "daemon off;"] 
