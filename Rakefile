name = "thesis"
$VERBOSE = nil

def mylog(msg = '')
	printf "\x1b[38;05;14m#{msg} finished."
	printf "\x1b[38;05;10m\n"
end

desc 'Multi tasks : [build, clean]'
task :default => ["build", 'clean']

desc "Update sections/**.tex and build/#{name}.pdf"
task :build do
	Dir.glob("sections.src/*.md").map do |md|
		tex = md.sub("sections.src", "sections").sub(".md", ".tex")
		`pandoc #{md} -o #{tex}`
	end
	mylog 'pandoc'
	puts `uplatex -kanji=UTF8 #{name}.tex`
	mylog 'uplatex'
	puts `dvipdfmx #{name}.dvi`
	mylog 'dvipdfmx'
	puts `mv #{name}.pdf build/`
end

desc 'Clean current directory files'
task :clean do
	`rm *.log`
	`rm *.dvi `
	mylog 'cleaning'
end
desc "Alias to open #{name}.pdf"
task :open do
	`open build/thesis.pdf`
end
