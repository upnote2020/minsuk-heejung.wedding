# minsuk-heejung.wedding



// 카카오페이 송금 버튼 이벤트 리스너
modalBody.querySelector('.kakao-pay-button').addEventListener('click', function() {
  // 계좌번호와 이름 가져오기
  const accountNumber = account.account;
  const accountHolder = account.holder;
  
  // 카카오페이 딥링크 생성
  // 참고: 실제 딥링크 포맷은 카카오페이 개발자 문서를 확인하세요
  const kakaoPayDeeplink = `kakaotalk://sendpayment?receiver=${encodeURIComponent(accountHolder)}&bank=${encodeURIComponent(account.bank)}&account=${encodeURIComponent(accountNumber)}&amount=&message=축의금`;
  
  // 모바일 기기에서만 작동
  if (/Android|iPhone|iPad|iPod/i.test(navigator.userAgent)) {
    window.location.href = kakaoPayDeeplink;
    
    // 앱이 열리지 않을 경우 타임아웃 후 스토어로 이동
    setTimeout(function() {
      if (confirm('카카오페이 앱이 설치되어 있지 않은 것 같습니다. 설치하시겠습니까?')) {
        if (/Android/i.test(navigator.userAgent)) {
          window.location.href = 'https://play.google.com/store/apps/details?id=com.kakao.talk';
        } else if (/(iPhone|iPad|iPod)/i.test(navigator.userAgent)) {
          window.location.href = 'https://apps.apple.com/kr/app/id362057947';
        }
      }
    }, 1500);
  } else {
    alert('모바일 기기에서만 카카오페이 송금이 가능합니다.');
  }
});

// 토스 송금 버튼 이벤트 리스너
modalBody.querySelector('.toss-button').addEventListener('click', function() {
  // 토스 송금 딥링크 생성
  // 참고: 실제 딥링크 포맷은 토스 개발자 문서를 확인하세요
  const tossDeeplink = `supertoss://send?bank=${encodeURIComponent(account.bank)}&accountNo=${encodeURIComponent(account.account)}&origin=송금&amount=&memo=축의금`;
  
  if (/Android|iPhone|iPad|iPod/i.test(navigator.userAgent)) {
    window.location.href = tossDeeplink;
    
    // 앱이 열리지 않을 경우 타임아웃 후 스토어로 이동
    setTimeout(function() {
      if (confirm('토스 앱이 설치되어 있지 않은 것 같습니다. 설치하시겠습니까?')) {
        if (/Android/i.test(navigator.userAgent)) {
          window.location.href = 'https://play.google.com/store/apps/details?id=viva.republica.toss';
        } else if (/(iPhone|iPad|iPod)/i.test(navigator.userAgent)) {
          window.location.href = 'https://apps.apple.com/kr/app/id839333328';
        }
      }
    }, 1500);
  } else {
    alert('모바일 기기에서만 토스 송금이 가능합니다.');
  }
});