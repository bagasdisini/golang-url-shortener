# Go URL Shortener

Simple and small URL shortener project using [Go](https://go.dev/) and [MySQL](https://www.mysql.com/).

## Installation

Clone this repository to your local storage.

```bash
git clone https://github.com/bagasdisini/golang-url-shortener
```

Make sure your MySQL database already started and create table `dblink` on it. If you want to use another database or just simply want to change table name, edit `pkg/mysql/mysql.go`.

```go
func DatabaseInit() {
	var err error

	// Connection to database, edit this code as you like
	connect := "root:@tcp(127.0.0.1:3306)/dblink?charset=utf8mb4&parseTime=True&loc=Local"
	DB, err = gorm.Open(mysql.Open(connect), &gorm.Config{})

	if err != nil {
		panic(err)
	}

	fmt.Println("Database Connected!")
}
```

If all preparations already finished, simply run `main.go` in your terminal and server will run in `http://localhost:5000/`.

```bash
go run main.go
```

## Usage

Open your favorite REST API Tester such as [Postman](https://www.postman.com/), [Insomnia](https://insomnia.rest/), [Paw](https://paw.cloud/), [cURL](https://curl.se/), etc.

### Generate Short URL From Input

Set URL to `http://localhost:5000/` and METHOD to `POST`. Send this JSON type in body, in this example we'll shorten [Facebook](https://www.facebook.com/) URL.

```json
{
    "long_url" : "https://www.facebook.com/"
}
```
Note : You can input any URL format to `long_url`, such as `http://www.abc.com`, `http://abc.com`, `www.abc.com`, `abc.com`

And if you got JSON return like this, you're successfully short your URL. Congrats! 🎉

```json
{
    "status_code": 200,
    "data": {
        "id": 1,
        "short_url": "http://localhost:5000/HzLQlbh",
        "long_url": "https://www.facebook.com/"
    }
}
```

### Getting Original URL From Short URL

Set URL to `http://localhost:5000/` and METHOD to `GET`. Send this JSON type in body, in this example we'll getting `http://localhost:5000/HzLQlbh` original URL.

```json
{
    "short_url" : "http://localhost:5000/HzLQlbh"
}
```
Note : You can ONLY input `http://www.abc.com` URL format to `short_url`.

And if you got JSON return like this, you're successfully getting your original URL. Woohooo! 🎉🎉

```json
{
    "status_code": 200,
    "data": {
        "id": 1,
        "short_url": "http://localhost:5000/HzLQlbh",
        "long_url": "https://www.facebook.com/"
    }
}
```

### Testing Short URL

Simply input your shorten URL in favorite web browser, press enter, and Violaa!! 🎉🎉🎉

## Authors

- [@bagasdisini](https://www.github.com/bagasdisini)

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)
