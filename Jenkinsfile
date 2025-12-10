// Jenkinsfile (scripted pipeline) untuk simple-python-pyinstaller-app
// Asumsi: Python 3 sudah ter-install dan bisa dipanggil dengan 'python'

node {
    stage('Checkout') {
        checkout scm
    }

    stage('Setup Python & Dependencies') {
        // Pastikan pip up to date dan pytest terpasang
        bat '''
python --version
python -m pip install --upgrade pip
python -m pip install pytest
'''
    }

    stage('Build') {
        // Compile file Python ke bytecode *.pyc
        bat '''
python -m py_compile sources/add2vals.py sources/calc.py
'''
    }

    stage('Test') {
        // Jalankan unit test pakai pytest dan buat laporan JUnit
        bat '''
python -m pytest --junitxml=test-results.xml
'''
        junit 'test-results.xml'
    }

    stage('Archive') {
        // Arsipkan hasil penting (misal bytecode)
        archiveArtifacts artifacts: 'sources/*.pyc, test-results.xml', fingerprint: true
    }
}
