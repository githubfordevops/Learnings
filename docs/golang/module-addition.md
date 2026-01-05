# Create the repo and initialize module

```
mkdir dir-name
cd dir-name
go mod init mod-name(usually same as dir-name)
```

This creates:
```
nf-lib/

└── go.mod
```

go.mod will look like:
```
module nf-lib

go 1.21
```

Run the below for all the dependencies to be downloaded:

`go mod tidy(optional)`
