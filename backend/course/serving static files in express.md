# Defining the root of the public file
Static files are the just the files that are sitting in our server like images, html, pdf, videos
inorder to access that files from the client(browser) we cannot directly do "baseurl/public/overview.html" we have to specify some routes or in express we can do that using a middleware

app.use(express.static("dir/public")) // like our static files is inside the public folder

when we access we just simply "baseurl/overview.htlm" we don't specify the public in the route simply because when we openup a url and server can't find any routes then it looks inside the public folder that we just defined the root in app.use(static('public'));