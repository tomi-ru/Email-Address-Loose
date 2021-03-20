# NAME

Email::Address::Loose - Make Email::Address->parse() loose

# SYNOPSIS

    my $address = 'read..rfc822.@docomo.ne.jp'; # Email::Addess can't find
    
    use Email::Address::Loose;
    my ($email) = Email::Address::Loose->parse($address); # find!

    use Email::Address;
    use Email::Address::Loose -override;
    my ($email) = Email::Address->parse($address); # find!
    

# DESCRIPTION

Email::Address::Loose is a [Email::Address](https://metacpan.org/pod/Email%3A%3AAddress), but `parse()` is "loose" same as
[Email::Valid::Loose](https://metacpan.org/pod/Email%3A%3AValid%3A%3ALoose).

This module is for web developers in Japan.

This module is needed because email address by the Japanese mobile carrier was
not RFC compliant. Fortunately, this evil spec was changed in April 2009(docomo),
October 2009(kddi). However email address that taken before 2009 is still available.
So this module is still needed.

ドコモやauがドットを連続で使ったり@マークの直前にドットを置くなど
RFC外のメールアドレスを許可していましたが、Email::Addressではそれをメールアドレスと
認識しません。このモジュールはそれらを許可するようにします。
現在はそのようなアドレスは新規に取れないようですが、以前に取ったものは使い続け
られているようなので、このモジュールを使っておいた方がいいでしょう。

# USAGE

    my ($email) = Email::Address::Loose->parse('docomo..taro.@docomo.ne.jp');
    print $email->address; # => "docomo..taro.@docomo.ne.jp"
    print $email;          # => "docomo..taro.@docomo.ne.jp" (as_string)
    print $email->user;    # => "docomo..taro."
    print $email->host;    # => "docomo.ne.jp"

Same as [Email::Address](https://metacpan.org/pod/Email%3A%3AAddress).

# IMPORT OPTION

- -override

        use Email::Address;
        use Email::Address::Loose -override;
         
        my ($email) = Email::Address->parse('docomo..taro.@docomo.ne.jp');
        print $email->address; # => "docomo..taro.@docomo.ne.jp"

    Call `globally_override()`(see below) at compile time.

# ORIGINAL METHODS

- globally\_override()

        Email::Address::Loose->globally_override;

    Changes `Email::Address->parse()` into `Email::Address::Loose->parse()`.

- globally\_unoverride()

        Email::Address::Loose->globally_unoverride;

    Restores override-ed `Email::Address->parse()`.

# SEE ALSO

[Email::Address](https://metacpan.org/pod/Email%3A%3AAddress), [Email::Valid::Loose](https://metacpan.org/pod/Email%3A%3AValid%3A%3ALoose) - this module based on these.

[Email::Address::JP::Mobile](https://metacpan.org/pod/Email%3A%3AAddress%3A%3AJP%3A%3AMobile) - will help you too.

\#mobilejp on irc.freenode.net (I've joined as "tomi-ru")

# AUTHOR

Naoki Tomita <tomita@cpan.org>

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.
