For hosting images:
cloudinary

For hosting site:
heroku
PostgreSQL database addon

For java: 
SpringBoot with JPA

For frontend: 
Vue 

### 1. **Heroku (Free Tier)**

Heroku is a popular platform-as-a-service (PaaS) that’s super beginner-friendly. It allows you to host **Spring Boot applications** and a database for free (within certain usage limits).

- **Spring Boot Hosting**: Heroku supports Java and Spring Boot directly, so you can deploy your backend easily.
- **Database**: Heroku provides a free **PostgreSQL** database through the **Heroku Postgres** add-on. This is great for small-scale projects, and the free tier should be sufficient for testing with a few users.

#### How to use Heroku:

1. **Create an account** on Heroku (it’s free).
2. Install the **Heroku CLI** on your machine to manage deployments.
3. Push your Spring Boot app to Heroku using Git.
4. **Add the PostgreSQL database** add-on in Heroku, which gives you a free Postgres database.

##### Example Workflow:

- Develop your Spring Boot app locally.
- Deploy the app to Heroku via the CLI (`git push heroku master`).
- Your app will be available online with a Heroku-provided URL (e.g., `https://your-app.herokuapp.com`).
- **PostgreSQL database** will be accessible via environment variables (`DATABASE_URL`) which you can configure in your Spring Boot `application.properties`.

#### Free Tier Limitations:

- Heroku's free tier **"sleeps"** if there’s no traffic for 30 minutes, which is fine for a demo or testing but might cause some initial delay when accessing the app after it has been inactive.
- The **PostgreSQL database** free tier has a limit of 10,000 rows, which should be plenty for a small test.