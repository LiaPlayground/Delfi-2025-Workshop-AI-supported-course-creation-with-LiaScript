# Makefile to concatenate all agent markdown files into team.md


TEAM_MD=team.md
AGENT_FILES=\
	agent/verlag.md \
	agent/analyse.md \
	agent/redaktion.md \
	agent/didaktik.md \
	agent/autor.md \
	agent/lektorat.md

all: $(TEAM_MD)

$(TEAM_MD): $(AGENT_FILES)
	rm -f $@
	for file in $(AGENT_FILES); do \
	  cat "$$file" >> $@; \
	  echo '\n\n\n' >> $@; \
	done

.PHONY: clean
clean:
	rm -f $(TEAM_MD)
