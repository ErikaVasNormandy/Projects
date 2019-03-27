# Nginx
 This is a skeleton guide on how to recreate the deployment used for Scavengers' Repo, Disaster Response, etc.
 Ingredients: 
 A host you can ssh into
 Install ssh
 
Update the repo with npm run build
This generates a new production folder that nginx automatically points to

Navigate to /etc/nginx/sites-available/default
```bash 
server {
        listen 80 default_server;
        listen [::]:80 default_server;


        root /home/admin0/reactive-frontend/build;
        server_name reactive.scavengers-repo.com
        index index.html

   # proxy_set_header X-Forwarded-Host $host;
   # proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

        server_name _;

        location / {
          if (!-e $request_filename){
            rewrite ^(.*)$ /index.html break;
         }


        }
        
          location /api/contents {

         proxy_pass http://reactive.scavengers-repo.com:5000/api/contents;

}



        location /api/projects{

         proxy_pass http://reactive.scavengers-repo.com:5000/api/projects;

}


        location /api/worldbuildings{
         proxy_pass http://reactive.scavengers-repo.com:5000/api/worldbuildings;

}

        location /api/artworks{
         proxy_pass http://reactive.scavengers-repo.com:5000/api/artworks;

}

        location /api/charsheets{
         proxy_pass http://reactive.scavengers-repo.com:5000/api/charsheets;

}

        ```
