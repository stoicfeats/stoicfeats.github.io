# stoic feats

personal website built with hugo, minimal design focused on learning, projects, and writings.

## quick start

```bash
# start development server
brew install hugo
make run
```

visit [http://localhost:1313](http://localhost:1313) in your browser.

## structure

```
content/
├── _index.md          # homepage
├── posts/             # blog posts
├── projects/          # project roadmap
├── learning/          # learning resources
│   ├── genai/        # generative ai
│   └── rag/          # retrieval-augmented generation
├── wisdom/            # thoughts & insights
└── resume/            # professional resume
```

## customization

- homepage: edit `content/_index.md`
- blog: add posts in `content/posts/`
- config: update `config.toml`
- style: modify `assets/css/main.scss`
