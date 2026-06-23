node {
    stage('Checkout') {
        // 본인의 GitHub 레포지토리 주소로 변경 필요
        git url: 'https://github.com/penny4bunny-lab/prac_4.git', branch: 'main', credentialsId: 'github-checkout-token'
    }

    stage('Build') {
        try {
            bat 'npm install' // 빌드 전 패키지 설치 보완
            bat 'npm run build' // React 기본 빌드 명령어로 보완
        } catch (e) {
            error '빌드 실패: ${e}'
        }
    }

    stage('Test') {
        // 지난 실습에서 확인한 Windows 환경 및 테스트 코드 없음 예외 처리 적용
        def testsPassed = bat(script: 'set CI=true && npm test -- --passWithNoTests', returnStatus: true)
        if (testsPassed != 0) {
            error '테스트 실패!'
        }
    }

    stage('Deploy') {
        if (env.BRANCH_NAME == 'main') {
            bat 'npm start'
        } else {
            echo 'Main 브랜치가 아니어서 실행 생략'
        }
    }
}
