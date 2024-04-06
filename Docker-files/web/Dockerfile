FROM nginx
LABEL "Project" = "vprofile"
LABEL "Author" = "Avraaj"

# Delete the nginx default configuration file
RUN rm -rf /etc/nginx/conf.d/default.conf

# Copy our configuration file
COPY nginvproapp.conf /etc/nginx/conf.d/vproapp.conf