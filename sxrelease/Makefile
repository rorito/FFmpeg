RELEASE := ffmpeg-$(shell git describe master)+$(shell git log --oneline master.. | wc -l)p

$(RELEASE).tar.xz: $(RELEASE).tar
	xz -k $^
	sha256sum $@
upload: $(RELEASE).tar.xz
	scp $^ pypi@pip.stupeflix.com:packages/sxffmpeg/
$(RELEASE).tar: patches-$(RELEASE)
	(cd .. && git archive --format=tar --prefix=$(RELEASE)/ HEAD > $(PWD)/$@)
	tar -r -f $@ patches-$(RELEASE)/*
patches-$(RELEASE):
	git format-patch master -o patches-$(RELEASE)
clean:
	$(RM) -r patches*
	$(RM) *.tar *.tar.xz
