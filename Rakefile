require 'pathname'
def project_path
  Pathname.new(File.dirname(__FILE__))
end

def build_path
  project_path + "build"
end

def output_path(format = :html)
  build_path + format.to_s
end

def output_images_path(format = :html)
  output_path(format) + "images"
end

def output_file(format = :html, ext = :html)
  output_path(format) + output_filename(ext)
end

def output_filename(ext = :html)
  "book.#{ext}"
end

def book_file
  # The version of the book with syntax highlighting turned on
  "book-highlights.adoc"
end

def formats
  %w(html pdf epub mobi docbook)
end

namespace :init do
  task :prepare do
    formats.each do |f|
      FileUtils.mkdir_p output_path(f)
    end
  end

  task :build, [:format, :ext, :command, :extra_args, :cleanup_images] => :prepare do |t, args|
    puts "Creating #{args[:format]} book"

    target = output_images_path(args[:format])
    FileUtils.mkdir_p(target)
    Dir[project_path + "ch*/images/**/*"].each do |source|
      FileUtils.cp(source, target)
    end

    system("bundle", "exec", args[:command], book_file,
           "-D", output_path(args[:format]).to_s, "-o", output_filename(args[:ext]).to_s,
           "-B", project_path.to_s,
           *args[:extra_args].split(" "))

    if args[:cleanup_images]
      FileUtils.rm_r(output_images_path(args[:format]))
    end
    puts "#{args[:format]} book created in #{output_file(args[:format], args[:ext])}"
  end

  desc 'Build HTML format'
  task :html do
    Rake::Task["init:build"].invoke("html", "html", "asciidoctor", "")
  end

  task :pdf do
    Rake::Task["init:build"].invoke("pdf", "pdf", "asciidoctor-pdf", "-a imagesdir=build/pdf", true)
  end

  task :epub do
    Rake::Task["init:build"].invoke("epub", "epub", "asciidoctor-epub3", "-a imagesdir=build/epub", true)
  end

  task :mobi do
    Rake::Task["init:build"].invoke("mobi", "mobi", "asciidoctor-epub3", "-a ebook-format=kf8 -a imagesdir=build/mobi", true)
  end

  task :all => formats do
    puts "Created all formats"
  end

  task :clean do
    `rm -rf #{build_path}`
  end
end

task :default => %w(init:clean init:html)
