start: 
	@echo "Stopping docker images (if running...)"
	docker-compose down
	@echo "Building (when required) and starting docker images..."
	docker-compose up --build 
	@echo "Docker images built and started!"
	
stop:
	@echo "Stopping docker compose..."
	docker-compose down
	@echo "Done!"

run_invoice : 
	cd ../invoice-service && go run ./cmd/main.go

createdb:
	docker exec -it project_postgres_1 createdb --username=postgres --owner=postgres invocing

opendb:
	docker exec -it project_postgres_1 psql -U postgres invoicing

dropdb:
	docker exec -it project_postgres_1 dropdb  --username=postgres invoicing


migrateup:
	migrate -path ../invoice-service/db/migration -database "postgres://postgres:password@localhost/invoicing?sslmode=disable" -verbose up

migratedown:
	migrate -path ../invoice-service/db/migration -database "postgres://postgres:password@localhost/invoicing?sslmode=disable" -verbose down 

# createmigration:
# 	migrate create -ext sql -dir db/migration -seq init_schema