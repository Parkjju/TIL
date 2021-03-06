# Jekyll 이용하여 블로그 개설하기 (MacOS 기준)

- [Reference : Jekyll공식문서](https://jekyllrb.com/)
- [Reference : 얼큰우동TV 지킬 기반의 Github Pages생성](https://www.youtube.com/channel/UCp-MztINXTRVkRGCnqnYNlQ)

## Installation

- Jekyll공식문서 DOCS메뉴의 QuickStart에서 prerequirements들어가서 확인

  1. Ruby 2.4.0이상 버전
  2. RubyGems
  3. GCC and MAKE

- 이용중인 OS에 맞게 guides에 들어간다.

### Installation - Jekyll on MacOS

- 모든작업은 맥의 터미널 앱을 통해 진행된다.

1. set SDKROOT
   - `export SDKROOT=$(xcrun --show-sdk-path)`
2. Install Ruby
   - `ruby -v`를 입력하여 루비 버전을 확인한다. (2.4.0 이상이여야 함, Big Sur의 경우 루비 2.6.3과 호환된다고 함)

```zsh
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Ruby
brew install ruby
```

- shell configuration에 루비와 gem 경로를 추가한다 (꼭 해줘야됨)

```zsh
# If you're using Zsh
echo 'export PATH="/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/3.0.0/bin:$PATH"' >> ~/.zshrc

# If you're using Bash
echo 'export PATH="/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/3.0.0/bin:$PATH"' >> ~/.bash_profile

# Unsure which shell you are using? Type
echo $SHELL
```

- **Ruby 가장 최신 버전 설치 후에 갖가지 조치를 취해봐도 버전 변경 불가 이슈는 여전히 남아있음. 추후 업데이트 필요시 확인**

3. Install Jekyll

- bundler와 jekyll gems를 설치한다. (해당 명령어를 입력해도 zsh: command not found 관련 오류가 발생하면 공식문서의 경로설정 부분을 다시 입력해보자. 구글링으로 삽질 해도 의미없었음)

```zsh
gem install --user-install bundler jekyll
```

```zsh
# If you're using Zsh
echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.zshrc

# If you're using Bash
echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.bash_profile

# Unsure which shell you are using? Type
echo $SHELL
```

- 경로까지 추가해주고 루비 및 gem의 설치가 완료된다.

4. Initialize

- 터미널 창을 통해 자신이 개설할 블로그메이킹 폴더로 진입한다.
- 해당 폴더에서 `bundle init`을 진행. -> Gemfile, Gemfile.lock이 생김

- 텍스트 에디터 툴 (Vscode 등)을 이용하여 Gemfile의 내용에 `gem "jekyll"`을 추가한다. (매우 중요! 터미널 창에 gem "jekyll"을 입력하는 것이 절대 아님)

- 모두 완료하였으면 html 작성하여 로컬서버 작동해보자.
  1. `jekyll build`
  2. `bundle exec jekyll serve`
