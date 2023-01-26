# LIN2_TE


cd /home/cpnv/TE_LIN2-main/api-server/

docker image build . -t lin2-server:v1

# impossible de faire tourner container en font
docker run -d -p 5000:5000 lin2-server:v1

docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' 5e2835


cd /home/cpnv/TE_LIN2-main/api-client/

docker image build . -t lin2-client:v1

docker login

docker tag lin2-server:v1 titanmanco/lin2-server:latest
docker push titanmanco/lin2-server:latest

docker tag lin2-client:v1 titanmanco/lin2-client:latest
docker push titanmanco/lin2-client:latest

cd ..
nano docker-compose.yml

docker compose up -d

docker build . -t enelg/tp2docker:v1 --no-cache
docker push enelg/tp2docker:v1
