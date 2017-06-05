BASE := $(subst -, ,$(notdir ${CURDIR}))
ORG  := geomesa
REPO := $(word 2, ${BASE})
IMG  := quay.io/${ORG}/${REPO}

build: dockerfile
	docker build \
		--build-arg TAG=${TAG} \
		-f target/Dockerfile \
		-t ${IMG}:${TAG} .

dockerfile:
	mkdir -p target
	sed 's/__TAG__/'"${TAG}"'/' Dockerfile.template > target/Dockerfile

publish: build
	docker push ${IMG}:${TAG}

test: build
	docker run -it --rm ${IMG}:${TAG} javac -version

clean:
	rm -rf target/