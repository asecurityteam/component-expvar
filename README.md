# component-expvar - Settings component for sending expvar metrics
[![GoDoc](https://godoc.org/github.com/asecurityteam/component-expvar?status.svg)](https://godoc.org/github.com/asecurityteam/component-expvar)


[![Bugs](https://sonarcloud.io/api/project_badges/measure?project=asecurityteam_component-expvar&metric=bugs)](https://sonarcloud.io/dashboard?id=asecurityteam_component-expvar)
[![Code Smells](https://sonarcloud.io/api/project_badges/measure?project=asecurityteam_component-expvar&metric=code_smells)](https://sonarcloud.io/dashboard?id=asecurityteam_component-expvar)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=asecurityteam_component-expvar&metric=coverage)](https://sonarcloud.io/dashboard?id=asecurityteam_component-expvar)
[![Duplicated Lines (%)](https://sonarcloud.io/api/project_badges/measure?project=asecurityteam_component-expvar&metric=duplicated_lines_density)](https://sonarcloud.io/dashboard?id=asecurityteam_component-expvar)
[![Lines of Code](https://sonarcloud.io/api/project_badges/measure?project=asecurityteam_component-expvar&metric=ncloc)](https://sonarcloud.io/dashboard?id=asecurityteam_component-expvar)
[![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=asecurityteam_component-expvar&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=asecurityteam_component-expvar)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=asecurityteam_component-expvar&metric=alert_status)](https://sonarcloud.io/dashboard?id=asecurityteam_component-expvar)
[![Reliability Rating](https://sonarcloud.io/api/project_badges/measure?project=asecurityteam_component-expvar&metric=reliability_rating)](https://sonarcloud.io/dashboard?id=asecurityteam_component-expvar)
[![Security Rating](https://sonarcloud.io/api/project_badges/measure?project=asecurityteam_component-expvar&metric=security_rating)](https://sonarcloud.io/dashboard?id=asecurityteam_component-expvar)
[![Technical Debt](https://sonarcloud.io/api/project_badges/measure?project=asecurityteam_component-expvar&metric=sqale_index)](https://sonarcloud.io/dashboard?id=asecurityteam_component-expvar)
[![Vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=asecurityteam_component-expvar&metric=vulnerabilities)](https://sonarcloud.io/dashboard?id=asecurityteam_component-expvar)


<!-- TOC -->

## Overview

This is a [`settings`](https://github.com/asecurityteam/settings) that enables
sending metrics for the values usually provided through the [Expvar HTTP
endpoints](https://golang.org/pkg/expvar/). We have extended the set of metrics
to also include the current goroutine count.

## Quick Start

```golang
package main

import (
    "context"
    "net/http"

    stat "github.com/asecurityteam/component-stat"
    expvar "github.com/asecurityteam/component-expvar"
    "github.com/asecurityteam/settings/v2"
)

func main() {
    ctx := context.Background()
    envSource := settings.NewEnvSource(os.Environ())

    s, _ := stat.New(ctx, envSource)
    exp, _ := expvar.Load(ctx, envSource, expvar.NewComponent().WithStat(s))
    defer exp.Close()
    go exp.Report()
}
```

## Status

This project is in incubation which means we are not yet operating this tool in
production and the interfaces are subject to change.

## Contributing

### Building And Testing

We publish a docker image called [SDCLI](https://github.com/asecurityteam/sdcli) that
bundles all of our build dependencies. It is used by the included Makefile to help
make building and testing a bit easier. The following actions are available through
the Makefile:

-   make dep

    Install the project dependencies into a vendor directory

-   make lint

    Run our static analysis suite

-   make test

    Run unit tests and generate a coverage artifact

-   make integration

    Run integration tests and generate a coverage artifact

-   make coverage

    Report the combined coverage for unit and integration tests

### License

This project is licensed under Apache 2.0. See LICENSE.txt for details.

### Contributing Agreement

Atlassian requires signing a contributor's agreement before we can accept a patch. If
you are an individual you can fill out the [individual
CLA](https://na2.docusign.net/Member/PowerFormSigning.aspx?PowerFormId=3f94fbdc-2fbe-46ac-b14c-5d152700ae5d).
If you are contributing on behalf of your company then please fill out the [corporate
CLA](https://na2.docusign.net/Member/PowerFormSigning.aspx?PowerFormId=e1c17c66-ca4d-4aab-a953-2c231af4a20b).
