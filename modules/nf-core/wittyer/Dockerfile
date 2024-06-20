FROM mcr.microsoft.com/dotnet/sdk:6.0@sha256:58cbcd2b7947cd770402492a588d37f0696ac5b8cbf320b4611e48ce7d1a8314 as builder
WORKDIR /src
COPY . /src
RUN cd Wittyer \
    && dotnet publish -f net6.0 -r linux-x64 -c Release -o /output \
    && chmod +x /output/Wittyer

FROM mcr.microsoft.com/dotnet/runtime:6.0@sha256:a579915e4f0e16d389b69b5de630bdd8e775bb9ca441700f3f72277a1fee6522
LABEL git_repository=https://git.illumina.com/DASTE/Ilmn.Das.App.Wittyer.git
WORKDIR /opt/Wittyer
RUN apt-get -y update && apt-get -y install tabix libunwind8 openssl procps
COPY --from=builder /output /opt/Wittyer
