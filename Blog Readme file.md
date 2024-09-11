# Personal Blog with Ruby on Rails

Welcome to my Blog project! This Ruby on Rails application allows you to create a blog where posts are rendered from Markdown files. It includes support for both English and Arabic languages and features a commenting system.


> [!NOTE] It's Live !
> You can visit the live project where I share my study notes and thoughts as I unravel the world of web on [hodasalim.com](https://www.hodasalim.com)

## Features

- **Multilingual Support**: Write and render blog posts in English and Arabic.
- **Markdown Support**: Use Markdown files for content creation.
- **Comments**: Users can comment on individual blog posts.
- **Language Selection**: Visitors can choose their preferred language for reading posts.
- **Simple and Clean UI**: A user-friendly interface for both reading and commenting on posts.

## Prerequisites

Before you begin, ensure you have the following installed:

- Ruby (version 3.1 or higher)
- Rails (version 7.0 or higher)
- SQLite (for development) or any other supported database for production

## Getting Started

Follow these steps to set up the project on your local machine.

1. **Clone the Repository**

   ```bash
   git clone https://github.com/yourusername/simple-blog.git
   cd simple-blog
   ```

2. **Install Dependencies**

   Ensure you have Bundler installed:

   ```bash
   gem install bundler
   ```

   Then install the required gems:

   ```bash
   bundle install
   ```

3. **Setup the Database**

   Create and migrate the database:

   ```bash
   rails db:create
   rails db:migrate
   ```

4. **Add Markdown Files**

   Place your Markdown files in the `app/posts` directory. Each Markdown file should be named with a language suffix to differentiate between English and Arabic versions:

   ```
   app/posts/post-title.en.md
   app/posts/post-title.ar.md
   ```

   Ensure that each file includes the necessary front matter to identify the language and other metadata.

5. **Configure Localization**

   - **Locale Files**: Add locale files for English and Arabic in `config/locales`. Example files could be `en.yml` and `ar.yml`.
   - **Language Switcher**: Implement a language switcher in the UI to allow visitors to select their preferred language.

6. **Start the Rails Server**

   Run the following command to start the development server:

   ```bash
   rails server
   ```

   You can now access your blog at `http://localhost:3000`.

## Usage

- **Viewing Posts**: Navigate to `http://localhost:3000/posts` to see a list of all posts.
- **Selecting Language**: Use the language switcher on the site to choose between English and Arabic.
- **Reading a Post**: Click on a post title to view the full content in the selected language.
- **Commenting**: At the bottom of each post, you will find a form to leave comments. Fill it out and submit to add your comment.

## Testing

To run tests, use the following command:

```bash
rails test
```

## Contributing

If you wish to contribute to this project, please fork the repository and submit a pull request with your changes. Make sure to include tests and documentation where applicable.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

For any questions or feedback, please contact me at [hoda.s.salim@gmail](mailto:hoda.s.salim@gmail.com).

---

This updated README outlines the steps for setting up a bilingual blog and explains how to handle Markdown files for different languages, as well as configuring a language switcher for users. Adjust the specifics based on your exact implementation details and requirements!


Hey this is a test to see if the characther limit exceeds 140 charachters what will happen I believe ti will be just fine as 