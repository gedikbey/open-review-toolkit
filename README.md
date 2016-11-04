# Open Review Toolkit

The [Open Review Toolkit](http://www.openreviewtoolkit.org/) enables you to convert your book manuscript into a website that can be used for Open Review. During the Open Review process everyone can read your manuscript and help make it better, and you can collect valuable feedback to improve the manuscript and help launch your book.

You can view a [sample site](http://sample.openreviewtoolkit.org/) generated by this repository.

## Getting Started

0. Download and install [Vagrant](https://www.vagrantup.com/).
1. Download the soure code by either cloning the git repository or downloading the [latest release](https://github.com/open-review-toolkit/open-review-toolkit/releases/latest).
2. Once you've cloned the git repository or extracted the release source code, open your favorite terminal and navigate to the directory the holds the source code. You should several files and directories in this directory, including a file call `Vagrantfile`.
3. From your terminal, run: `vagrant up`. The very first time you run this command it will download roughly 1.5GB of data, so it may take some time depending on the speed of your internet connection.
4. Once the previous command has completed, run `vagrant ssh`. You are now inside the Vagrant VM, which includes all the dependencies for the project.
5. `make book` will create a PDF file of the book and place it in the `output/` directory.
6. `make site` will build an Open Review site from the book. After building the site, you can view it in your browser by visiting: http://0.0.0.0:17278/. This link only works on your local machine. See the Publishing Your Site section before for how to publish your site publicly.

As you make changes to the Markdown files, you will need to re-run the relevant `make` command above in order to re-build the PDF and/or site. Once you're done working with the Vagrant VM, it's a good idea to shut it down with `vagrant halt`. The next time you want to start again, you can run `vagrant up` and `vagrant ssh`.

## Modification Tips

**Reminder:** after any of these modifications, you'll need to re-run the appropriate `make` command to re-build the PDF or site.

The [sample site](http://sample.openreviewtoolkit.org/) includes some details on how to modify your site.

In order configure the site to use your Google Analytics account, you must update the `ga_code` configuration item in `website/config.rb`.

### Setting up email collection with Google Forms

The sample site includes some email collection forms, which can interact with [Google Forms](https://www.google.com/forms/about/). Here are the steps for setting that up:

1. Create a new blank Google Form.
2. Give the form a title.
3. Create a question named "Email" that accepts a "Short answer".
4. Click the "Preview" link for the form (eye icon).
5. Copy URL of the form preview.
6. Inside the Vagrant VM (via `vagrant ssh`), execute `./scripts/google-form-details.rb`.
7. Paste URL from the form preview page when the script asks for it and press enter.
8. Update the `config[:google_form_action]` setting in `website/config.rb` with the URL specified as the "Form action".
9. Update the `config[:google_form_email_field]` setting in `website/config.rb` with the value associated with your email field from the script output.

After running `make site`, you should be able to test that everything is working and see your email address show up in the "Responses" tab of your Google Form. You can also download the responses as a CSV.

## Publishing Your Site

After running `make site`, the complete website is available as static HTML pages and assets in the `website/build/` directory. These can be copied over to the web host of your choice. You can also use a static web site host like [GitHub Pages](https://pages.github.com/).
