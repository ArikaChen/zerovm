# it fails sometime, i think, since "cp" have a little time
# to finish copy before zerovm read it
NAME=copy
CCFLAGS=-n -s -nostartfiles -nostdlib -fno-builtin

all: $(NAME).c
	@x86_64-nacl-gcc -o $(NAME).nexe $(CCFLAGS) -Wall -msse4.1 \
	-O2 -I$(ZEROVM_ROOT) -I$(ZEROVM_ROOT)/tests/functional $^
	@sed 's#PWD#$(PWD)#g' $(NAME).template > $(NAME).manifest
	@mkfifo input.data
	@cp $(NAME).nexe input.data&
	@$(ZEROVM_ROOT)/zerovm $(NAME).manifest

clean:
	rm -f $(NAME).nexe $(NAME).o *.log *.data *.manifest
