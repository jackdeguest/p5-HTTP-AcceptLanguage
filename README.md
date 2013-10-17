# NAME

HTTP::AcceptLanguage - Accept-Language header parser and find available language

# HOW DO I USE THIS MODULE WITH

## WITH CGI.pm

    use HTTP::AcceptLanguage;
    my $lang = HTTP::AcceptLanguage->new($ENV{HTTP_ACCEPT_LANGUAGE})->match(qw/ en fr es ja zh-tw /);

## WITH raw PSGI

    use HTTP::AcceptLanguage;
    my $lang = HTTP::AcceptLanguage->new($env->{HTTP_ACCEPT_LANGUAGE})->match(qw/ en fr es ja zh-tw /);

## WITH Plack::Request

    use HTTP::AcceptLanguage;
    my $lang = HTTP::AcceptLanguage->new($req->header('Accept-Language'))->match(qw/ en fr es ja zh-tw /);

# SYNOPSIS

Good example of the input and output.

    # If language quality is the same then order by match method's input list
    my $accept_language = HTTP::AcceptLanguage->new('en;q=0.5, ja;q=0.1');
    $accept_language->match(qw/ th da ja /); # -> ja
    $accept_language->match(qw/ en ja /);    # -> en

    my $accept_language = HTTP::AcceptLanguage->new('en, da');
    $accept_language->match(qw/ da en /); # -> en
    $accept_language->match(qw/ en da /); # -> en

You can obtain the order of preference of the available languages ​​list of client

    my $accept_language = HTTP::AcceptLanguage->new('en, ja;q=0.3, da;q=1, *;q=0.29, ch-tw');
    $accept_language->languages; # -> en, da, ch-tw, ja, *

You can use the 0.01 version spec. (next version is deplicated)

    local $HTTP::AcceptLanguage::MATCH_PRIORITY_0_01_STYLE = 1;
    

    my $accept_language = HTTP::AcceptLanguage->new('en, da');
    $accept_language->match(qw/ da en /); # -> da
    $accept_language->match(qw/ en da /); # -> en

# DESCRIPTION

HTTP::AcceptLanguage is HTTP Accept-Language header parser And you can find available language by Accept-Language header.

# METHODS

## new($ENV{HTTP\_ACCEPT\_LANGUAGE})

It to specify a string of Accept-Language header.

## match(@available\_language)

By your available language list, returns the most optimal language.

If language-quality has the same value, is a priority order of the new($ENV{HTTP\_ACCEPT\_LANGUAGE}).

## languages

Returns are arranged in order of quality language list parsed.

# AUTHOR

Kazuhiro Osawa <yappo {at} shibuya {dot} pl>

# COPYRIGHT

Copyright 2013- Kazuhiro Osawa

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# SEE ALSO

RFC2616, [I18N::AcceptLanguage](http://search.cpan.org/perldoc?I18N::AcceptLanguage)
