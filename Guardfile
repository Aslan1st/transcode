# A sample Guardfile
# More info at https://github.com/guard/guard#readme

## Uncomment and set this to only include directories you want to watch
#directories %w(app lib config test spec features) \
#  .select{|d| Dir.exists?(d) ? d : UI.warning("Directory #{d} does not exist")}

## Note: if you are using the `directories` clause above and you are not
## watching the project directory ('.'), then you will want to move
## the Guardfile to a watched dir and symlink it back, e.g.
#
#  $ mkdir config
#  $ mv Guardfile config/
#  $ ln -s config/Guardfile .
#
# and, you'll have to watch "config/Guardfile" instead of "Guardfile"

# Example 1: Run a single command whenever a file is added
=begin
notifier = proc do |title, _, changes|
  Guard::Notifier.notify(changes * ",", title: title )
end

guard :yield, { run_on_additions: notifier, object: "Add missing specs!" } do
  watch(/^(.*)\.rb$/) { |m| "spec/#{m}_spec.rb" }
end

# Example 2: log all kinds of changes


require 'logger'
yield_options = {
  object: ::Logger.new(STDERR), # passed to every other call

  start: proc { |logger| logger.level = Logger::INFO },
  stop: proc { |logger| logger.info "Guard::Yield - Done!" },

  run_on_modifications: proc { |log, _, files| log.info "!! #{files * ','}" },
  run_on_additions: proc { |log, _, files| log.warn "++ #{files * ','}" },
  run_on_removals: proc { |log, _, files| log.error "xx #{files * ','}" },
}

guard :yield, yield_options do
  watch(/^(.*)\.css$/)
  watch(/^(.*)\.jpg$/)
  watch(/^(.*)\.png$/)
end
=end

convert_to_cfr = proc do |_, _, file|
  file_path = 'C:/Users/Aslan/Desktop/Transcode/videos/output/'
  #procedure for checking if ffmpeg is already encodig a file
  running = proc do
    output = `tasklist /fi "imagename eq ffmpeg.exe"`
    not_running = "INFO: No tasks are running which match the specified criteria.\n"
    if output == not_running
      false
    else
      true
    end
  end
  file.each do |f|
  unless running.call
    sleep(1)
  end
  new_file = File.basename("#{f}", ".mp4")
  system "ffmpeg -i #{f} -r 30 #{file_path}#{new_file}_edit.mp4"
  end
end

guard :yield, { run_on_additions: convert_to_cfr } do
  watch(/^(.*)\.mp4$/) {|m| File.expand_path("#{m[0]}")}
end
