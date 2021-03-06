            
	※ 알고리즘 설명
	
		A, B, C 좌표를 기준으로 상하좌우를 탐색하면서 색상 개수를 구해보는 알고리즘 입니다.
			
===========================================================================================================	

	
		for(int i = A; i < X; i++)
            color[0][(i - A) % N]++;
        for(int i = A - 1; i >= 0; i--)
            color[0][(A - i) % N]++;
			
		>> A, B, C 기준에서 앞뒤 큐브의 색상 개수를 구합니다.
===========================================================================================================


		long sum = 0;
        long quotient = (offset - 1 - criteria) / N;
        long remain = (offset - 1 - criteria) % N;
		
		>> 1을 빼준 이유는 기준점을 제외하고 계산하기 위함입니다.
		>> 몫(quotient)를 구해서 몇 번 반복이 되는지 찾습니다.
		   - 2번 TestCase를 직접 손으로 해보면 일정한 값이 하나씩 밀리는 것을 볼 수 있습니다.
		     기준점 좌표를 빼주고 몫을 구하면 몇 번 반복되는지 알 수 있습니다.
		>> 나머지(remain)는 반복되지 않는 경우를 처리하기 위함입니다.
===========================================================================================================	
	
	
		for(int i = 0; i < N; i++)
			sum += color[idx - 1][i];
			
		>> 이전 좌표에서 얻은 색상값을 모두 합쳐줍니다.
		   왜냐하면 색상 값이 일정한 규칙으로 반복되기 때문에 계산을 쉽게하기 위해서입니다.
===========================================================================================================		   
		
		
		for(int i = 0; i < N; i++)
            color[idx][i] = (sum * quotient) + color[idx - 1][i];
         
        for(int i = 1; i <= remain; i++) {
            for(int j = 0; j < N; j++)
                color[idx][(i + j) % N] += color[idx - 1][j];
        }
		
		>> 몫(quotient)와 합산(sum)값을 곱해주고 따로 기준점을 더해주면
		   현재 좌표에서 N만큼의 큐브가 칠해진 색상값을 구할 수 있습니다. 
		>> 나머지는 반복이 되지 않기 때문에 따로 구해줍니다.
===========================================================================================================		
		
		
		quotient = criteria / N;
        remain = criteria % N;
         
        for(int i = 0; i < N; i++)
            color[idx][i] += (sum * quotient);
         
        for(int i = 1; i <= remain; i++) {
            for(int j = 0; j < N; j++)
                color[idx][(i + j) % N] += color[idx - 1][j];
        }
		
		>> 위와 비슷한 코드인데 위는 아래쪽을 해당 코드는 위쪽을 검사하는 로직입니다.
===========================================================================================================		
		