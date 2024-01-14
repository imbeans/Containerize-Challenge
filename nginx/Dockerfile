# Use the official Nginx base image
FROM nginx

# Create a non-root user
RUN useradd -m beans

# Switch to the non-root user
USER beans

# Expose ports 80 and 443
EXPOSE 80
EXPOSE 443

# Command to run Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
