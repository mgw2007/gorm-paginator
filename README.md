# gorm-paginator

## Usage

```bash
go get  github.com/mgw2007/gorm-paginator/paginator
```

```go
type User struct {
	ID       int
	UserName string `gorm:"not null;size:100;unique"`
}

var users []User
db = db.Where("id > ?", 0)

paginator.Pagging(&paginator.Param{
    DB:      db,
    Page:    1,
    Limit:   3,
    OrderBy: []string{"id desc"},
}, &users)
```

## With Gin

```go
r := gin.Default()
r.GET("/", func(c *gin.Context) {
    page, _ := strconv.Atoi(c.DefaultQuery("page", "1"))
    limit, _ := strconv.Atoi(c.DefaultQuery("limit", "3"))
    var users []User

    paginatorr,err := paginator.Pagging(&paginator.Param{
        DB:      db,
        Page:    page,
        Limit:   limit,
        OrderBy: []string{"id desc"},
        ShowSQL: true,
    }, &users)
    if(err != nil){
        c.JSON(500, err)
    }
    c.JSON(200, paginatorr)
})
```

## License

[MIT](LICENSE)
