package main

import (
	"fmt"
	"net/http"
)

func main() {
	
	http.HandleFunc("/", homeHandler)
	http.HandleFunc("/about", aboutHandler)
	http.HandleFunc("/contact", contactHandler)

	fmt.Println("Starting server on port 8080...")
	http.ListenAndServe(":8080", nil)
}


func homeHandler(w http.ResponseWriter, r *http.Request) {
	
	w.Header().Set("Content-Type", "text/html")

	
	fmt.Fprint(w, "<h1>Welcome to my home page!</h1>")
}

func aboutHandler(w http.ResponseWriter, r *http.Request) {
	
	w.Header().Set("Content-Type", "text/html")

	fmt.Fprint(w, "<h1>About Me</h1><p>I am a web developer.</p>")
}


func contactHandler(w http.ResponseWriter, r *http.Request) {

	w.Header().Set("Content-Type", "text/html")


	if r.Method == "POST" {

		name := r.FormValue("name")
		email := r.FormValue("email")
		message := r.FormValue("message")


		fmt.Printf("Name: %s\nEmail: %s\nMessage: %s\n", name, email, message)


		fmt.Fprint(w, "<h1>Thanks for contacting me!</h1>")
	} else {
	
		fmt.Fprint(w, "<h1>Contact Me</h1><form method='POST'><label>Name:</label><input type='text' name='name'><br><label>Email:</label><input type='email' name='email'><br><label>Message:</label><textarea name='message'></textarea><br><button type='submit'>Send</button></form>")
	}
}
