# What's an Operating System?

-   SSH(secure shell)

    -   protocol implemented(시행된) by other programs to securely access one computer from another.
    -   다른 컴퓨터에서 한 컴퓨터로 안전하게 액세스하기 위해 프로그램에 의해 구현된 프로토콜
    -   protocol? 복수의 컴퓨터 사이나 중앙 컴퓨터와 단말기 사이에서 데이터 통신을 원활하게 하기 위해 필요한 통신 규약.
    -   SSH를 사용하려면, SSH 서버에 연결하려는 컴퓨터에 SSH클라이언트가 설치되어있어야 함.
    -   SSH 서버는 특정 기계가 아니고 소프트웨어임
    -   원격 시스템에서, SSH 서버는 background process로 실행되고있다. (background process -> 사용자 간섭 없이 보이지 않는 뒷편에서 실행 중인 컴퓨터 프로세스) -> **It constantly checks if a client is trying to connect to it, then will authenticate its requests.**
    -   most popular program to use SSH -> 리눅스 내의 OpenSSH, 윈도우에서는 PuTTY

-   SSH 사용

    -   원격 대상 컴퓨터에 계정이 있어야됨. + 해당 컴퓨터의 호스트 이름 or IP주소도 필요
    -   the authenticity of host and then the IP address can't be established. 메세지의 출력 -> 이전에 이 컴퓨터에 연결한 적이 없고, SSH 클라이언트는 연결하려는 컴퓨터를 확인하거나 연결할 수 없다는 뜻
    -   메세지 출력 이후 올바른 원격 연결이면 yes -> 알려진 호스트로 저장되어 이후 메세지 출력 X
    -   SSH를 통해 연결되었으므로 원격 장치에서의 텍스트 명령 입력 -> SSH 서버로 전달. (APP실행 가능, 셀 환경에서 작업대신 GUI를 통한 작업도 가능)
    -   비밀번호를 통한 SSH연결은 보안상 안전하지 않음. -> SSH 인증 키를 사용
    -   SSH authentication key -> private key + public key
    -   public key -> can only lock something, private key -> can only unlock something

-   원격 시스템에 연결 (2) -> VPN이용
    -   VPN (virtual private network) - 멀리 떨어진 네트워크 환경을 안전한 네트워크로 만드는 역할
    -   ex) 회사 내부에서만 접근가능한 네트워크를 집에서 접속하기 위해 VPN을 이용.
