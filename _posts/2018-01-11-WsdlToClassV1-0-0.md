---
title: WsdlToClass V1.0.0 released
date: 2018-01-11 21:46:28
layout: post
tags: WsdlToClass
---
After spending some time in December on my WsdlToClass project it now has become a proper generator to be used when implementing an SOAP API based on an WSDL file.

On of the latest issues I wanted to resolve actually had me realise I had overlooked a very important issue. It wasn't PSR-4 compliant. With this being one of the key features of modern PHP this was something I really needed to fix.

With a little help from the [Nikic php-parser](https://github.com/nikic/PHP-Parser) the correct namespace and classname from the generated code can be derived in order to write the generated code to the correct file name. As a benefit anyone can alter the template or create its own and it will be written to the correct file location.

Hoping with [wsdl2phpgenerator](https://github.com/wsdl2phpgenerator/wsdl2phpgenerator) and [BeSimpleSoap](https://github.com/BeSimple/BeSimpleSoap/issues) seeming no longer to be maintained WsdlToClass would become a good starting place for generating PHP from a WSDL file.

If your missing a feature; run into issues or have a extravagant WSDL file which can break the generator call me out on [Twitter](https://twitter.com/EchteDanny); [GitHub](https://github.com/DannyvdSluijs/WsdlToClass) or send me an email @ [danny.vandersluijs@icloud.com](mailto:danny.vandersluijs@icloud.com)