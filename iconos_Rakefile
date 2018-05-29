# Add your own tasks in files placed in lib/tasks ending in .rake,
# for example lib/tasks/capistrano.rake, and they will automatically be available to Rake.

require File.expand_path('../config/application', __FILE__)

require "bundler/gem_tasks"

require 'sprite_factory'

ROOT_PATH = File.dirname(__FILE__)

Empleate::Application.load_tasks

namespace :assets do
  desc 'recreate sprite images and css'
  task :resprite do
    SpriteFactory.library = :chunkypng
    SpriteFactory.csspath = "image-path('sprites/$IMAGE')"
    dirs = Dir.glob("#{ROOT_PATH}/app/assets/images/sprites/*/")
    dirs.each do |path|
      dir_name = path.split("/").last
      SpriteFactory.run!("app/assets/images/sprites/#{dir_name}",
                          :layout => :packed,
                          :output_style => "app/assets/stylesheets/#{dir_name}.scss",
                          :nocomments => true,
                          :selector => ".#{dir_name}-") do |images|
        result = []
        images.each do |img|
          result << ".social-share-button-#{img[0]} { display:inline-block; #{img[1][:style]} }"
        end
        result.join("\n")
      end
    end
  end
end
