default: fmt lint install generate

internal/provider: provider_code_spec.json
	#tfplugingen-framework generate all --input provider_code_spec.json --output internal/provider
	echo hi
	
provider_code_spec.json: generator.yaml openapi-schema.json	
	tfplugingen-openapi generate --config generator.yaml --output provider_code_spec.json openapi-schema.json
	
build: internal/provider
	go build -v ./...

install: build
	go install -v ./...

lint:
	golangci-lint run

generate:
	cd tools; go generate ./...

fmt:
	gofmt -s -w -e .

test:
	go test -v -cover -timeout=120s -parallel=10 ./...

testacc:
	TF_ACC=1 go test -v -cover -timeout 120m ./...

.PHONY: fmt lint test testacc build install generate internal/provider
