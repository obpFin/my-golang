postgres:
	docker run --name postgres12 -p 5432:5432 -e POSTGRES_USER=root -e POSTGRES_PASSWORD=secret -d postgres:12-alpine

psql:
	docker exec -it postgres12 psql -U root

createdb:
	 docker exec -it postgres12  createdb --username=root --owner=root simple_bank

startdb:
	docker start postgres12

dropdb:
	 docker exec -it postgres12  dropdb simple_bank

migrateup:
	migrate -path db/migration -database "postgresql://root:secret@localhost:5432/simple_bank?sslmode=disable" -verbose up

migratedown:
	migrate -path db/migration -database "postgresql://root:secret@localhost:5432/simple_bank?sslmode=disable" -verbose down

pullsqlc:
	docker pull kjconroy/sqlc

sqlcinit:
	docker run --rm -v $$(pwd):/src -w /src kjconroy/sqlc init

sqlcgenerate:
	docker run --rm -v $$(pwd):/src -w /src kjconroy/sqlc generate

test:
	go test -v -cover ./...

server:
	go run main.go

.PHONY: postgres psql createdb startdb dropdb migrateup migratedown sqlcinit sqlcgenerate test server