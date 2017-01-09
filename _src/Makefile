
MD_FILES = $(shell find *.md)
HTML_FILES = $(MD_FILES:%.md=../%.html)

all: $(HTML_FILES)

clean:
	rm -f $(HTML_FILES)

../%.html: %.md
	grip --export $< $@

