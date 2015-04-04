require 'travis'

def restart_travis(repo)
  lb = Travis::Repository.find(ENV[repo]).last_build
  checkpr = lb.attributes['pull_request']
  lb_name = lb.branch_info
  if lb_name == 'master'
    lb.restart
  else
    if checkpr
      Travis::Repository.find(ENV[repo]).branches['master'].restart
    else
      lb.restart
      Travis::Repository.find(ENV[repo]).branches['master'].restart
    end
  end
end

desc "Builds the ENV['TRAVIS_REPOSITORY'] travis job with token ENV['TRAVIS_TOKEN']"
task :stravis do
  Travis.access_token = ENV['TRAVIS_TOKEN']

  repos = ['TRAVIS_REPO_ENIGMA','TRAVIS_REPO_RSUNLIGHT','TRAVIS_REPO_COWSAY',
    'TRAVIS_REPO_ANALOGSEA']

  repos.each do |iter|
    restart_travis(iter)
  end
end
