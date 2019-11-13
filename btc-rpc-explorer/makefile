.PHONY: build
build:
	@docker build -t prakashr1984/explorer . 

.PHONY: stop
stop: 
	@docker stop explorer || true

.PHONY: remove
remove: stop
	@docker rm explorer || true

.PHONY: run
run: remove
	@docker run --name explorer -d  \
	--network host \
	--restart unless-stopped \
	prakashr1984/explorer

.PHONY: logs
logs:
	@docker logs -f explorer --tail 1000

.PHONY: rmi
rmi:
	@docker rmi -f $(shell docker images -a --filter=dangling=true -q) || true

.PHONY: rm
rm:
	@docker rm $(shell docker ps -a -f status=exited -q) || true

.PHONY: clean
clean: rmi rm
	@echo "cleanup done!!"