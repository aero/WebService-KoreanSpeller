# NAME

WebService::KoreanSpeller - Korean spellchecker

# SYNOPSIS

    use WebService::KoreanSpeller;
    use utf8;

    my $checker = WebService::KoreanSpeller->new( text=> '안뇽하세요? 방갑습니다.' );
    my @results = $checker->spellcheck;   # returns array of hashes
    binmode STDOUT, ':encoding(UTF-8)';
    foreach my $item (@results) {
        print $item->{position}, "\n";    # index in the original text (starting from 0)
        print $item->{incorrect}, " -> "; # incorrect spelling
        print $item->{correct}, "\n";     # correct spelling
        print $item->{comment}, "\n";     # comment about spelling
        print "------------------------------\n";
    }


    OUTPUT:

    0
    안뇽하세요 -> 안녕하세요
    표준 발음·표준어 오류
    어린이들의 발음을 흉내내어 '안뇽'이라고 말하는 사람들이 종종 있습니다. 특히, 글을 쓸 때에는 이러한 단어를 쓰지 않도록 합시다.
    ------------------------------
    7
    방갑습니다 -> 반갑습니다
    약어 사용 오류
    오늘날 통신에서 자주 쓰는 은어입니다.
    ------------------------------

# DESCRIPTION

This module provides a Perl interface to the Web-based korean speller service( 온라인 한국어 맞춤법/문법 검사기 - http://speller.cs.pusan.ac.kr ).

# METHODS

## new( text => 'text for spell check' )

Returns an obejct instance of this module. text should be "Unicode string"(a.k.a. perl's internal format - utf8 encoding/utf8 flag on)

## spellcheck

Returns results as array of hashes(if there is no error in the text, this method will return empty list), See SYNOPSIS. you can easily convert AoH to JSON or XML.

# CAUTION

I'm afraid we don't have a good open source korean spell checker. but there is a decent proprietary service that runs on the online website( 온라인 한국어 맞춤법/문법 검사기 - http://speller.cs.pusan.ac.kr ). So I made this module with web-scrapping approach, this is easy to mess up if they change layout of the website. Let me know if this does not work. \*This module follows the same terms of the original service agreement.\*

# AUTHOR

C.H. Kang <chahkang@gmail.com>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2012 by C.H. Kang.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
